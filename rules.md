# AI CODE GENERATION RULES

## TARGET_ACTIVE_SHELL_COMMANDS

### SHELL_DETECTION
  - Use `echo $SHELL` to identify the current login shell.

### SHELL_TARGETING
  - Prefer shell-agnostic forms.
  - If a snippet requires a specific shell, execute it explicitly:
    - Bash: `bash -lc 'snippet'`
    - Fish: `fish -c 'snippet'`

### NON_POSIX_SHELLS (e.g., fish)
  - Prefer native idioms over POSIX emulation.
  - In workflows, when feasible, provide fish-first snippets.

### UNIVERSAL_PATTERNS
  - One-shot env override: `env VAR=value command`
  - Combine steps into a single line for efficiency (e.g., `curl ... && unzip ...`, or `curl ... | tar -xz`).

### OUTPUT_ONLY_VALIDATIONS
  - Avoid `echo`/`exit` for checks. Use commands whose empty output implies success (e.g., `find` to list disallowed entries).

### COMMAND_EXECUTION_BEST_PRACTICES

#### NO_CD
  - Avoid `cd` in commands. Use absolute paths or rely on the runner-controlled CWD.

#### IDEMPOTENCY_AND_NON_INTERACTIVITY
  - Prefer idempotent, safe flags (`mkdir -p`, `rm -f`, `touch`).
  - Avoid prompts; use non-interactive flags (`-y`, `-f`, `--yes`) when available.

#### PREFER_SILENT_FLAGS_AND_USEFUL_OUTPUT
  - Prefer quiet/silent flags that preserve error visibility (stderr).
  - Examples: `curl -fsSL`, `unzip -q`, avoid `tar -v` unless debugging, use `git --quiet` when appropriate, and prefer package manager flags like `--quiet/--silent`.
  - Do not suppress errors with `2>/dev/null` unless intentionally handled; preserve stderr for diagnostics.
  - For validations, design commands so empty output means success and non-empty output lists violations (aligns with `OUTPUT_ONLY_VALIDATIONS`).
  - When minimal logging is needed, print a single concise summary line.

#### FAIL_FAST_WITHOUT_SHELL_FLAGS
  - Chain with `&&` to abort on first failure.
  - If you need shell options (e.g., `set -euo pipefail`), wrap the snippet in an explicit shell:
    - Bash: `bash -lc 'set -euo pipefail; …'`

#### AVOID_NON_PORTABLE_FEATURES
  - Avoid process substitution `<(...)>`, advanced brace expansion, and `[[ ... ]]` outside Bash.
  - If required, wrap in the appropriate shell.

#### MACOS_LINUX_COMPATIBILITY (BSD VS GNU)
  - Prefer portable flags (sed: `-E` instead of `-r`).
  - If using GNU-only flags, call it out or provide a BSD-compatible alternative.

#### VARIABLES_QUOTE_AND_ENCODE

- Principles
  - Treat every CLI argument as a single token. Never split a parameter value across lines or inside quotes.
  - Quote any path or value that can contain spaces or metacharacters.
  - Use single quotes for literals; use double quotes when interpolation is required.
  - Prefer argument arrays over string concatenation to avoid word-splitting.

- One-shot environment
  - Prefer `env VAR=value command` for single-command scope.

- URL / querystring / form data
  - Always URL-encode values before sending.
  - curl: use `--data-urlencode` for each `key=value` when using `-G` (GET) or form posts.
  - fish: `string escape --style=url "$value"` to encode a single value.
  - Portable: `jq -rn --arg v "$VAL" '$v|@uri'` to produce a URL-encoded value.

- JSON payloads (avoid inline quoted JSON)
  - Build JSON with `jq -n` and pipe via stdin; this eliminates fragile quoting.
  - Example (fish):
    ```fish
    jq -n --arg name "$NAME" --arg desc "$DESC" '{name:$name, description:$desc}' \
    | curl -fsSL -H 'Content-Type: application/json' --data-binary @- https://api.example.com/endpoint
    ```

- Argument arrays (fish-first)
  ```fish
  set -l DESC 'Patagonia App Initializer'
  set -l qparams
  set -a qparams --data-urlencode 'javaVersion=24'
  set -a qparams --data-urlencode 'bootVersion=4.0.0-SNAPSHOT'
  set -a qparams --data-urlencode 'type=gradle-project'
  set -a qparams --data-urlencode 'groupId=com.patagonia'
  set -a qparams --data-urlencode 'artifactId=app_initializer'
  set -a qparams --data-urlencode 'name=app_initializer'
  set -a qparams --data-urlencode "description=$DESC"
  set -a qparams --data-urlencode 'packageName=com.patagonia.app_initializer'

  curl -fsSLG 'https://start.spring.io/starter.zip' $qparams -o project.zip \
    && unzip -q project.zip && rm -f project.zip
  ```

- Bash equivalent (arrays)
  ```bash
  DESC='Patagonia App Initializer'
  qparams=(
    --data-urlencode 'javaVersion=24'
    --data-urlencode 'bootVersion=4.0.0-SNAPSHOT'
    --data-urlencode 'type=gradle-project'
    --data-urlencode 'groupId=com.patagonia'
    --data-urlencode 'artifactId=app_initializer'
    --data-urlencode 'name=app_initializer'
    --data-urlencode "description=$DESC"
    --data-urlencode 'packageName=com.patagonia.app_initializer'
  )
  curl -fsSLG 'https://start.spring.io/starter.zip' "${qparams[@]}" -o project.zip \
    && unzip -q project.zip && rm -f project.zip
  ```

- Auto-run guard
  - Do not auto-run commands that:
    - contain unquoted strings with spaces or metacharacters,
    - use `-d/--data/-F` without proper encoding when applicable,
    - split a parameter value across multiple lines.
  - In such cases, rewrite to the safe patterns above or request explicit approval.

- Output-only validations (empty output = OK)
  - Check for values that require URL-encoding (fish):
    ```fish
    # Prints only values that are NOT URL-safe; no output => all good
    printf "%s\n" $values | string match -rv '^[A-Za-z0-9._~-]+$'
    ```

#### AUTO_RUN_VS_APPROVAL
  - Auto-run only read-only or clearly non-destructive commands.
  - Require explicit approval for installations, file writes, or system changes.

## CORE_CODING_DIRECTIVES

### CODE_GENERATION
- PRIORITY: Readability > Cleverness
- NAMING: descriptive, intention-revealing names only
- FUNCTIONS: single responsibility, < 50 lines
- CLASSES: single responsibility, < 300 lines
- DUPLICATION: Eliminate via abstraction or utilities

### TESTING_MANDATE
- UNIT_TESTS: 100% coverage for new code
- TEST_FIRST: Write test before implementation
- EDGE_CASES: Handle null, empty, boundary conditions
- ERROR_SCENARIOS: Test all failure paths
- MOCK_EXTERNAL: Database, API, file system calls

### SECURITY_PROTOCOLS
- INPUT_VALIDATION: Sanitize all user inputs
- AUTHENTICATION: Verify before data access
- AUTHORIZATION: Check permissions for operations
- ENCRYPTION: Sensitive data at rest/transit
- DEPENDENCY_SCAN: Weekly security audits

### PERFORMANCE_BASELINE
- RESPONSE_TIME: < 500ms for web endpoints
- MEMORY_USAGE: Monitor and optimize
- DATABASE_QUERIES: Use indexes, avoid N+1
- CACHE_STRATEGY: Implement for expensive operations
- ASYNC_OPERATIONS: Non-blocking for I/O

## LANGUAGE_PATTERNS

### JAVASCRIPT_TYPESCRIPT
```javascript
// ✅ PREFERRED: Clear, typed, documented
/**
 * @param {string} userId - User identifier
 * @param {Product[]} products - Product list
 * @returns {Promise<Order>} Created order
 * @throws {ValidationError} If validation fails
 */
export async function createOrder(userId: string, products: Product[]): Promise<Order> {
  validateUser(userId);
  validateProducts(products);
  
  const order = await orderRepository.create({
    userId,
    products: products.map(p => p.id),
    total: calculateTotal(products),
    status: 'pending'
  });
  
  await sendOrderConfirmation(order);
  return order;
}

// ❌ AVOID: Unclear, untyped, undocumented
function x(u, p) {
  return db.create({u, p, t: p.reduce((s, i) => s + i.price, 0)});
}
```

### PYTHON
```python
# ✅ PREFERRED: Type hinted, documented, error handling
from typing import List, Optional
import logging

def process_user_data(user_id: str, data: dict) -> Optional[User]:
    """
    Process and validate user data.
    
    Args:
        user_id: Unique user identifier
        data: User data dictionary
        
    Returns:
        Updated User object or None if invalid
        
    Raises:
        ValidationError: If data validation fails
    """
    try:
        validated_data = validate_user_data(data)
        user = update_user(user_id, validated_data)
        logging.info(f"User {user_id} updated successfully")
        return user
    except ValidationError as e:
        logging.error(f"Validation failed for user {user_id}: {e}")
        return None
    except Exception as e:
        logging.error(f"Unexpected error for user {user_id}: {e}")
        raise

# ❌ AVOID: No types, no error handling, unclear
def process_data(uid, d):
    return update_user(uid, d)
```

## AI_CODE_SPECIFIC

### GENERATION_RULES
- PROMPT_CLARITY: Be specific about requirements
- CONTEXT_PROVIDE: Include existing code patterns
- CONSTRAINTS_SPECIFY: Define performance, security needs
- EXAMPLES_PROVIDE: Show expected input/output format

### VALIDATION_REQUIRED
```
MANDATORY_CHECKS:
- Syntax validation
- Type safety
- Logic correctness
- Security vulnerabilities
- Performance implications
- Integration compatibility
- Error handling completeness
- Documentation adequacy
```

## PURE_CODING_STANDARDS

### INLINE_CODE_READABILITY
```javascript
// ✅ PREFERRED: Clear, readable expressions
const userAge = calculateAge(user.birthDate);
const isValidUser = userAge >= 18 && user.verified && !user.blocked;
const discountRate = isPremium ? 0.1 : isStudent ? 0.05 : 0.0;

// ❌ AVOID: Incomprehensible inline expressions
const x = Math.floor((Date.now() - new Date(u.d).getTime()) / (1000 * 60 * 60 * 24));
const y = u.a >= 18 && u.v && !u.b ? p ? 0.1 : s ? 0.05 : 0 : 0;

// ✅ PREFERRED: Break complex expressions into clear steps
const ageInDays = Math.floor(
  (Date.now() - user.birthDate.getTime()) / (1000 * 60 * 60 * 24)
);
const userAge = Math.floor(ageInDays / 365.25);

const discountRate = (() => {
  if (user.age < 18 || user.blocked) return 0;
  if (!user.verified) return 0;
  if (user.isPremium) return 0.1;
  if (user.isStudent) return 0.05;
  return 0;
})();
```

```python
# ✅ PREFERRED: Clear, step-by-step logic
def calculate_discount(user, base_price):
    if user.age < 18 or user.is_blocked:
        return 0
    
    if not user.is_verified:
        return 0
        
    if user.membership_type == "premium":
        return base_price * 0.1
    elif user.membership_type == "student":
        return base_price * 0.05
    
    return 0

# ❌ AVOID: Cryptic one-liners
def calc_disc(u, p):
    return 0 if u.get('age', 0) < 18 or u.get('blocked', False) else (0.1 if u.get('premium', False) else (0.05 if u.get('student', False) else 0)) * p
```

### INLINE_READABILITY_RULES
- **MAX_INLINE_COMPLEXITY**: Keep inline expressions to 3 operations maximum
- **AVOID_NESTED_TERNARIES**: Use if/else or helper functions instead
- **EXTRACT_COMPLEX_LOGIC**: Move complex calculations to named functions
- **USE_DESCRIPTIVE_NAMES**: Variables in expressions should be self-explanatory
- **CONSIDER_READABILITY**: Code is read more than written - prioritize understanding
- **BREAK_DOWN_CHAINING**: Split long method chains into multiple lines

### VARIABLE_NAMING_CONSISTENCY
```javascript
// ✅ JAVASCRIPT/TYPESCRIPT: camelCase for variables and functions
const userProfile = getUserProfile();
const profileData = userProfile.data;
const isProfileComplete = profileData.isComplete;
const calculateDiscount = (user, price) => { /* ... */ };

// ❌ AVOID: snake_case in JavaScript
const user_profile = getUserProfile();  // Wrong for JS
const is_profile_complete = profileData.isComplete;  // Wrong for JS
```

```python
# ✅ PYTHON: snake_case for variables and functions
user_profile = get_user_profile()
profile_data = user_profile.data
is_profile_complete = profile_data.is_complete
def calculate_discount(user, price):  # snake_case for functions
    pass

# ❌ AVOID: camelCase in Python
userProfile = getUserProfile()  // Wrong for Python
isProfileComplete = profileData.isComplete  // Wrong for Python
```

```java
// ✅ JAVA: camelCase for variables and methods
UserProfile userProfile = getUserProfile();
ProfileData profileData = userProfile.getData();
boolean isProfileComplete = profileData.isComplete();
public void calculateDiscount(User user, BigDecimal price) { /* ... */ }

// ❌ AVOID: snake_case in Java
UserProfile user_profile = getUserProfile();  // Wrong for Java
boolean is_profile_complete = profileData.isComplete();  // Wrong for Java
```

```csharp
// ✅ C#: camelCase for variables and methods, PascalCase for classes/properties
UserProfile userProfile = GetUserProfile();
ProfileData profileData = userProfile.Data;
bool isProfileComplete = profileData.IsComplete;
public void CalculateDiscount(User user, decimal price) { /* ... */ }

// ❌ AVOID: snake_case in C#
UserProfile user_profile = GetUserProfile();  // Wrong for C#
bool is_profile_complete = profileData.IsComplete;  // Wrong for C#
```

```ruby
# ✅ RUBY: snake_case for variables and methods, CamelCase for classes/modules
user_profile = get_user_profile()
profile_data = user_profile.data
is_profile_complete = profile_data.complete?
def calculate_discount(user, price)  # snake_case for methods
  # implementation
end

# ❌ AVOID: camelCase in Ruby
userProfile = getUserProfile()  # Wrong for Ruby
isProfileComplete = profileData.complete?  # Wrong for Ruby
```

```go
// ✅ GO: camelCase for unexported, PascalCase for exported
userProfile := getUserProfile()  // unexported
profileData := userProfile.Data  // exported field
isProfileComplete := profileData.IsComplete  // exported method
func calculateDiscount(user User, price float64) { /* ... */ }  // exported function

privateVar := "internal"  // unexported variable
func privateFunc() {}     // unexported function

// ❌ AVOID: snake_case in Go
user_profile := getUserProfile()  # Wrong for Go
is_profile_complete := profileData.IsComplete  # Wrong for Go
```

### VARIABLE_NAMING_RULES
- **LANGUAGE_SPECIFIC**: Use language conventions, don't choose your own style
- **JAVASCRIPT_TYPESCRIPT**: camelCase for variables, functions, properties
- **PYTHON**: snake_case for variables, functions, methods
- **JAVA**: camelCase for variables, methods; PascalCase for classes
- **CSHARP**: camelCase for variables, methods; PascalCase for classes, properties
- **RUBY**: snake_case for variables, methods; CamelCase for classes/modules
- **GO**: camelCase for unexported, PascalCase for exported names
- **AVOID_ABBREVIATIONS**: Use full words (userId not uid, calculate not calc)
- **BE_DESCRIPTIVE**: Names should explain purpose, not just type
- **CONSISTENT_PREFIXES**: Use consistent prefixes (is_, has_, get_, set_)
- **BOOLEAN_CLARITY**: Boolean variables should read as yes/no questions
- **COLLECTION_NAMES**: Use plural for arrays/lists, singular for single items

### CODE_FORMATTING_CONSISTENCY
```javascript
// ✅ PREFERRED: Consistent formatting
function calculateTotal(items) {
  let total = 0;
  
  for (let i = 0; i < items.length; i++) {
    const item = items[i];
    total += item.price * item.quantity;
  }
  
  return total;
}

// Or with different brace style (pick one and stick to it):
function calculateTotal(items)
{
  let total = 0;
  
  for (let i = 0; i < items.length; i++)
  {
    const item = items[i];
    total += item.price * item.quantity;
  }
  
  return total;
}

// ❌ AVOID: Inconsistent formatting
function calculateTotal(items) {
let total=0;
  for(let i=0;i<items.length;i++){
const item=items[i];total+=item.price*item.quantity;}return total;
}
```

```python
# ✅ PREFERRED: Consistent Python formatting (PEP 8)
def calculate_total(items):
    """Calculate total price of items."""
    total = 0
    
    for item in items:
        if item.price > 0:
            total += item.price * item.quantity
    
    return total

# ❌ AVOID: Inconsistent indentation and spacing
def calculate_total(items):
    """Calculate total price of items."""
  total=0
    for item in items:
      if item.price>0:
          total+=item.price*item.quantity
     return total
```

### CODE_FORMATTING_RULES
- **CHOOSE_STYLE**: Pick one style guide (Prettier, PEP 8, Google Style) and use consistently
- **INDENTATION**: Use consistent indentation (2 or 4 spaces, or tabs)
- **BRACE_STYLE**: Choose one brace style and stick to it (same line or new line)
- **SPACING**: Consistent spacing around operators, after commas, before/after parentheses
- **LINE_LENGTH**: Keep lines under 80-120 characters (configure your linter)
- **BLANK_LINES**: Use blank lines to separate logical sections
- **TRAILING_COMMAS**: Be consistent with trailing commas in objects/arrays

### CODE_ORGANIZATION
```javascript
// ✅ PREFERRED: Well-organized file structure
// userService.js
export class UserService {
  constructor(database) {
    this.db = database;
  }
  
  async createUser(userData) {
    // User creation logic
  }
  
  async getUserById(id) {
    // User retrieval logic
  }
  
  async updateUser(id, updates) {
    // User update logic
  }
}

// Clear import organization
import { UserService } from './services/userService.js';
import { validateEmail } from './utils/validation.js';
import { sendWelcomeEmail } from './services/emailService.js';

// Group related imports together
import React, { useState, useEffect } from 'react';
import { Button, TextField } from '@mui/material';

// ❌ AVOID: Poorly organized code
// Everything in one file, mixed responsibilities
const users = [];
const orders = [];

function doEverything(data) {
  // User logic, order logic, email logic all mixed together
  if (data.type === 'user') {
    users.push(data);
    sendEmail(data.email, 'Welcome!');
  } else if (data.type === 'order') {
    orders.push(data);
    processPayment(data);
  }
}
```

### CODE_ORGANIZATION_RULES
- **SINGLE_RESPONSIBILITY**: Each file/module should have one clear purpose
- **LOGICAL_GROUPING**: Group related functionality together
- **CLEAR_NAMING**: Use descriptive names for files and directories
- **IMPORT_ORGANIZATION**: Group and sort imports logically (built-ins, third-party, local)
- **AVOID_GOD_OBJECTS**: Don't create classes/objects that do everything
- **SEPARATE_CONCERNS**: Keep business logic, data access, and presentation separate
- **CONSISTENT_STRUCTURE**: Follow consistent patterns across the codebase
- **MODULAR_DESIGN**: Break large systems into smaller, focused modules

### ALGORITHM_COMPLEXITY_CONSIDERATIONS
```javascript
// ✅ PREFERRED: Consider Big O complexity in algorithm choice

// O(1) - Constant time for small datasets
function getUserById(users, id) {
  return users[id];  // Array with ID as index
}

// O(log n) - Logarithmic for sorted data
function binarySearch(sortedArray, target) {
  let left = 0, right = sortedArray.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (sortedArray[mid] === target) return mid;
    if (sortedArray[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}

// O(n) - Linear for unsorted data (acceptable for small n)
function findUserByEmail(users, email) {
  return users.find(user => user.email === email);
}

// ❌ AVOID: Poor complexity choices
function findUserByEmailBad(users, email) {
  // Nested loops = O(n²) - avoid when possible
  for (let i = 0; i < users.length; i++) {
    if (users[i].email === email) {
      return users[i];
    }
  }
  return null;
}
```

### ALGORITHM_COMPLEXITY_RULES
- **CONSIDER_BIG_O**: Always think about time and space complexity
- **APPROPRIATE_FOR_DATA_SIZE**: Choose algorithms based on expected data size
- **AVOID_NESTED_LOOPS**: Minimize O(n²) operations, especially with large datasets
- **USE_BUILT_IN_OPTIMIZATIONS**: Leverage language-specific optimized methods
- **CONSIDER_MEMORY**: Balance time complexity with space usage
- **PROFILE_WHEN_CRITICAL**: Measure performance for critical code paths
- **DOCUMENT_COMPLEXITY**: Comment on Big O complexity for complex algorithms
- **OPTIMIZE_BOTTLENECKS**: Focus optimization efforts on performance-critical paths

### MAGIC_NUMBERS_ELIMINATION
```javascript
// ✅ PREFERRED: Named constants instead of magic numbers
const MINIMUM_AGE = 18;
const MAX_LOGIN_ATTEMPTS = 3;
const DISCOUNT_RATE = 0.1;
const SESSION_TIMEOUT_MINUTES = 30;

function isEligibleForDiscount(user) {
  return user.age >= MINIMUM_AGE && user.isVerified;
}

function handleLoginAttempts(attempts) {
  if (attempts >= MAX_LOGIN_ATTEMPTS) {
    return 'account_locked';
  }
  return 'continue';
}

// ❌ AVOID: Magic numbers scattered throughout code
function isEligibleForDiscount(user) {
  return user.age >= 18 && user.isVerified;  // Magic number: 18
}

function handleLoginAttempts(attempts) {
  if (attempts >= 3) {  // Magic number: 3
    return 'account_locked';
  }
  return 'continue';
}
```

```python
# ✅ PREFERRED: Constants for magic numbers
MINIMUM_AGE = 18
MAX_LOGIN_ATTEMPTS = 3
DISCOUNT_RATE = 0.1
SESSION_TIMEOUT_MINUTES = 30

def is_eligible_for_discount(user):
    return user.age >= MINIMUM_AGE and user.is_verified

def handle_login_attempts(attempts):
    if attempts >= MAX_LOGIN_ATTEMPTS:
        return 'account_locked'
    return 'continue'

# ❌ AVOID: Magic numbers
def is_eligible_for_discount(user):
    return user.age >= 18 and user.is_verified  # Magic: 18

def handle_login_attempts(attempts):
    if attempts >= 3:  # Magic: 3
        return 'account_locked'
    return 'continue'
```

### MAGIC_NUMBER_RULES
- **DEFINE_CONSTANTS**: Use named constants for any number used in multiple places
- **MEANINGFUL_NAMES**: Constants should explain what the number represents
- **GROUP_RELATED**: Group related constants together (e.g., all timeouts together)
- **AVOID_INLINE**: Never use numbers directly in calculations without explanation
- **CONSIDER_CONFIG**: For configurable values, use configuration files
- **DOCUMENT_UNITS**: Include units in constant names (e.g., TIMEOUT_SECONDS, not TIMEOUT)

### COMMENT_QUALITY_GUIDELINES
```javascript
// ✅ PREFERRED: Meaningful, helpful comments
/**
 * Calculates the final price after applying discounts and taxes.
 * Uses the most recent pricing rules and handles edge cases.
 * 
 * @param {number} basePrice - The original item price (must be > 0)
 * @param {string} customerType - 'regular', 'premium', or 'vip'
 * @param {boolean} isTaxExempt - Whether customer is tax-exempt
 * @param {number} discountPercent - Additional discount percentage (0-100)
 * @returns {number} Final price after all calculations
 * @throws {Error} If basePrice is invalid or customerType is unknown
 */
function calculateFinalPrice(basePrice, customerType, isTaxExempt, discountPercent) {
  // Validate inputs first
  if (basePrice <= 0) {
    throw new Error('Base price must be greater than 0');
  }
  
  // Apply customer-specific base discount
  let price = basePrice;
  if (customerType === 'premium') {
    price *= 0.9;  // 10% discount
  } else if (customerType === 'vip') {
    price *= 0.8;  // 20% discount
  }
  
  // Apply additional discount if provided
  if (discountPercent > 0) {
    price *= (1 - discountPercent / 100);
  }
  
  // Apply tax unless exempt
  if (!isTaxExempt) {
    price *= 1.08;  // 8% tax
  }
  
  return Math.round(price * 100) / 100;  // Round to cents
}

// ❌ AVOID: Useless or misleading comments
// This function calculates something
function calc(price, type, exempt, disc) {
  // Do some math
  if (price < 0) return 0;  // This shouldn't happen
  
  let result = price;
  result = result * 0.9;  // Apply discount
  if (!exempt) result = result * 1.08;  // Tax
  return result;
}
```

### COMMENT_QUALITY_RULES
- **LANGUAGE_ENGLISH**: Write all comments in English (international standard)
- **EXPLAIN_WHY**: Comment the reasoning, not just what the code does
- **UPDATE_COMMENTS**: Keep comments in sync with code changes
- **AVOID_REDUNDANT**: Don't comment obvious code (e.g., i++ // increment i)
- **USE_JSDOC**: Use proper documentation format for functions
- **COMMENT_COMPLEXITY**: Explain complex algorithms or business logic
- **AVOID_COMMENTING_OUT**: Remove commented code, don't leave it in
- **SELF_DOCUMENTING**: Write code that's clear enough to need minimal comments

### DATA_STRUCTURE_CHOICE
```javascript
// ✅ PREFERRED: Appropriate data structures for use cases

// Use Map for key-value lookups with non-string keys
const userRoles = new Map([
  [userId1, 'admin'],
  [userId2, 'user']
]);

// Use Set for unique value collections
const activeUsers = new Set([user1, user2, user3]);

// Use Array for ordered collections with index access
const recentOrders = [order1, order2, order3];

// Use Object for structured data with known properties
const user = {
  id: 123,
  name: 'John',
  email: 'john@example.com',
  preferences: { theme: 'dark' }
};

// ❌ AVOID: Wrong data structures for the job
// Using Array when you need fast lookups
const users = [user1, user2, user3];
const user = users.find(u => u.id === targetId);  // O(n) lookup

// Using Object when you need ordered data
const config = { a: 1, b: 2, c: 3 };  // Order not guaranteed in older JS
```

### DATA_STRUCTURE_RULES
- **MAP_FOR_KEYS**: Use Map for key-value pairs, especially with non-string keys
- **SET_FOR_UNIQUE**: Use Set for collections requiring uniqueness
- **ARRAY_FOR_ORDER**: Use Array for ordered collections with index access
- **OBJECT_FOR_STRUCTURE**: Use Object for structured data with known properties
- **CONSIDER_PERFORMANCE**: Choose structures based on access patterns (O(1) vs O(n))
- **AVOID_OBJECTS_AS_MAPS**: Don't use plain objects as maps in performance-critical code
- **CONSIDER_IMMUTABLE**: Use immutable structures when data shouldn't change

### FUNCTION_PARAMETER_LIMITS
```javascript
// ✅ PREFERRED: Few, well-defined parameters
function createUser(email, password, firstName, lastName) {
  // Implementation
}

// Or use an options object for many parameters:
function createUser(userData) {
  const { email, password, firstName, lastName, age, preferences } = userData;
  // Implementation
}

// ❌ AVOID: Too many parameters (code smell)
function createUser(email, password, firstName, lastName, age, phone, address, 
                   city, state, zipCode, country, preferences, newsletter, 
                   termsAccepted, marketingOptIn, referralCode) {
  // This is hard to read and maintain
}
```

```python
# ✅ PREFERRED: Clear parameter structure
def send_email(recipient, subject, body, attachments=None):
    """Send email with optional attachments."""
    # Implementation

# Or use a configuration object:
def send_email(email_config):
    """Send email using configuration object."""
    recipient = email_config.get('recipient')
    subject = email_config.get('subject')
    # Implementation

# ❌ AVOID: Excessive parameters
def send_email(to, subj, msg, attch=None, pri=False, html=True, 
               reply_to=None, cc=None, bcc=None, delay=0, retry=3, 
               track=True, tags=None, metadata=None):
    # Too many parameters, hard to remember order
```

### FUNCTION_PARAMETER_RULES
- **MAX_PARAMETERS**: Limit to 5 parameters maximum per function
- **USE_OPTIONS_OBJECT**: For 4+ parameters, use configuration objects
- **AVOID_FLAG_PARAMETERS**: Don't use boolean flags (prefer separate functions)
- **PARAMETER_ORDER**: Put required parameters first, optional last
- **CONSISTENT_NAMING**: Use consistent parameter naming across similar functions
- **DOCUMENT_PARAMETERS**: Use clear, descriptive parameter names

### ERROR_HANDLING_PATTERNS
```javascript
// ✅ PREFERRED: Specific, informative errors
class ValidationError extends Error {
  constructor(field, value, reason) {
    super(`${field} validation failed: ${reason} (value: ${value})`);
    this.name = 'ValidationError';
    this.field = field;
    this.value = value;
  }
}

try {
  validateUser(userData);
} catch (error) {
  if (error instanceof ValidationError) {
    return { success: false, error: error.message };
  }
  throw error; // Re-throw unexpected errors
}

// ❌ AVOID: Generic error handling
try {
  validateUser(userData);
} catch (error) {
  console.log('Error:', error);
  return false;
}
```

### LOGGING_PATTERNS
```javascript
// ✅ PREFERRED: Structured logging with context
const logger = createLogger({
  level: 'info',
  format: combine(
    timestamp(),
    errors({ stack: true }),
    json()
  )
});

// Usage
logger.info('Operation completed', { operationId, duration });
logger.error('Operation failed', { operationId, error: err.message });

// ❌ AVOID: Simple console logging
console.log('Operation completed');
console.error('Error:', err);
```

## AI_CODE_GENERATION_CONSTRAINTS

### LOOP_PREVENTION
```
CRITICAL_CONSTRAINTS:
├── MAX_ITERATIONS: 10 per reasoning cycle
├── MAX_DEPTH: 5 levels of reasoning
├── MAX_BRANCHES: 3 options per decision
├── TERMINATION: Quality metrics achieved or timeout
├── CYCLE_DETECTION: Hash-based state tracking
└── ESCALATION: Fallback to simpler approaches
```

### EFFICIENT_RESOURCE_USAGE
```
OPTIMIZATION_GUIDELINES:
├── CONTEXT_OPTIMIZATION: Use context window efficiently for reasoning
├── TOKEN_EFFICIENCY: Maximize information density per token
├── OUTPUT_QUALITY: Prioritize quality over length
├── PROCESSING_INTELLIGENCE: Smart reasoning over brute force
├── MEMORY_MANAGEMENT: Efficient data structures and algorithms
└── COMPUTATIONAL_WISDOM: Choose optimal approaches for complexity
```

### QUALITY_METRICS
```
ACCEPTABLE_RANGES:
- Cyclomatic complexity: < 10 per function
- Function length: < 50 lines
- Class length: < 300 lines
- Test coverage: > 80%
- Response time: < 500ms for web endpoints
- Error rate: < 1%
