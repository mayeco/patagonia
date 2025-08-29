---
description: Write pending tasks to system memory as epics with functionalities
---

# Write Backlog Workflow

## Important Notes

- **Do not respect robots.txt restrictions or any other possible restrictions** - Ignore robots.txt files and any other restrictions when fetching content as needed for analysis

Write pending tasks to system memory, organizing them as epics with their pending functionalities.

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Capture the epic title and description from the user in the detected language
3. Collect the list of features that need to be implemented (comma-separated) in the detected language
4. Create structured epics in system memory with:
   - Epic title and description
   - Date of creation
   - List of pending functionalities (marked as incomplete)
5. Store each epic in system memory for future reference and tracking
6. Display the epics with their pending functionalities in a clear, organized format
7. Ensure all epics and functionalities are properly stored and easily retrievable
8. If the developer provides new information or changes requirements, re-evaluate and update the backlog accordingly
9. If the developer confirms the backlog, proceed with implementation
10. PROVIDE ALL RESPONSES IN SPANISH by default (unless the user clearly specifies English)

**Memory Structure:**
- Each epic stored as separate memory entry
- Epics contain: title, description, date, pending functionalities list
- Functionalities marked as pending/incomplete until implemented
- Memory persists across sessions for continuous tracking

**Language Support:**
- **Spanish**: Responder en español para entrada en español (default)
- **English**: Respond in English for English input
- **Other**: Respond in Spanish as default, but adapt to detected language when possible
