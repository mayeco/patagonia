---
description: Create high-level epics that contain multiple features and user stories
---

# Write Epic Workflow

Create high-level epics that contain multiple features and user stories. Epics are large initiatives that span multiple development cycles and contain related features.

## ⚠️ CRITICAL AI EXECUTION RULES

**DO NOT GET STUCK IN ANALYSIS LOOPS**: Complete epic creation within 6 steps maximum.

**DECISION POINTS**: Make binary decisions - epic scope is appropriate or too broad.

**TERMINATION CONDITIONS**:

- If no epic description provided: Ask and STOP
- If epic is too vague: Ask for more details and STOP
- Always require developer confirmation before creating

## STEPS

{% include _includes/language-detection.md %}

1. **EPIC CAPTURE**:
   - Ask the developer for epic title and high-level description
   - Validate epic represents multiple features (not a single feature)
   - If too narrow: STOP - "This seems like a feature, not an epic"

2. **EPIC TYPE DETECTION**:
   - Analyze epic description for type indicators:
     - **Strategic**: Keywords like "strategic", "business goal", "company objective", "market expansion"
     - **Operational**: Keywords like "operational", "process improvement", "efficiency", "workflow"
     - **Technical**: Keywords like "technical", "architecture", "infrastructure", "platform"
     - **Product**: Keywords like "product", "user experience", "feature set", "customer value"
     - **Compliance**: Keywords like "compliance", "regulatory", "security", "standards"
   - Validate epic type against description
   - If unclear: Ask the developer to specify epic type and STOP

3. **SCOPE DEFINITION**:
   - Identify major themes and user goals based on epic type
   - Define success criteria and business value
   - **Strategic**: Business impact, ROI, market positioning
   - **Operational**: Efficiency gains, cost reduction, process optimization
   - **Technical**: Technical debt reduction, scalability, maintainability
   - **Product**: User satisfaction, feature adoption, competitive advantage
   - **Compliance**: Regulatory compliance, security posture, audit readiness
   - Estimate epic timeline (weeks/months, not days)

4. **STAKEHOLDER ANALYSIS**:
   - Identify primary stakeholders based on epic type
   - **Strategic**: Executive team, product leadership, key customers
   - **Operational**: Department heads, process owners, end users
   - **Technical**: Development teams, architects, DevOps
   - **Product**: Product managers, UX designers, customer success
   - **Compliance**: Legal, security, compliance officers
   - Assess stakeholder impact and communication needs
5. **FEATURE BREAKDOWN**:
   - Identify 3-7 major features within the epic based on epic type
   - Create placeholder user stories for each feature
   - Prioritize features by business value and stakeholder impact
   - Identify dependencies between features
   - Estimate effort and timeline for each feature

6. **SUCCESS METRICS DEFINITION**:
   - Define specific KPIs based on epic type:
     - **Strategic**: Revenue impact, market share, customer acquisition
     - **Operational**: Efficiency metrics, cost savings, process time reduction
     - **Technical**: Performance benchmarks, error rates, technical debt reduction
     - **Product**: User engagement, feature adoption, satisfaction scores
     - **Compliance**: Audit results, security assessments, compliance coverage
   - Set measurable success criteria and acceptance thresholds

7. **RISK ASSESSMENT**:
   - Identify epic-specific risks based on type:
     - **Strategic**: Market changes, competitive response, resource availability
     - **Operational**: Process disruption, training requirements, change resistance
     - **Technical**: Technical complexity, integration challenges, scalability issues
     - **Product**: User acceptance, feature usability, market fit
     - **Compliance**: Regulatory changes, security vulnerabilities, audit findings
   - Define mitigation strategies and contingency plans
8. **EPIC STRUCTURE CREATION**:
   - Create epic with title, description, success criteria
   - List major features and user stories
   - Include stakeholder analysis and success metrics
   - Assign unique epic identifier

9. **DEVELOPER CONFIRMATION**:
   - Present the complete epic structure
   - Ask for explicit confirmation to create
   - If declined: STOP without creating

10. **EPIC STORAGE**:

- Save to `/epics/{{date}}-{{epic_name | slugify}}.md`
- Confirm creation was successful
- Suggest next steps (break into projects or features)

## Epic Type Implementation Guidelines

### **Strategic Epic**

- **Focus**: Business growth, market expansion, competitive advantage
- **Timeline**: 3-12 months
- **Success Criteria**: Revenue impact, market share growth, strategic objectives
- **Stakeholders**: Executives, board members, key customers

### **Operational Epic**

- **Focus**: Process optimization, efficiency improvement, cost reduction
- **Timeline**: 2-6 months
- **Success Criteria**: Efficiency metrics, cost savings, process improvements
- **Stakeholders**: Department heads, process owners, end users

### **Technical Epic**

- **Focus**: Architecture modernization, technical debt reduction, scalability
- **Timeline**: 3-9 months
- **Success Criteria**: Performance improvements, technical debt reduction, scalability gains
- **Stakeholders**: Development teams, architects, DevOps engineers

### **Product Epic**

- **Focus**: User experience enhancement, feature development, product growth
- **Timeline**: 2-8 months
- **Success Criteria**: User satisfaction, feature adoption, product metrics
- **Stakeholders**: Product managers, UX designers, customer success teams

### **Compliance Epic**

- **Focus**: Regulatory compliance, security enhancement, audit readiness
- **Timeline**: 1-6 months
- **Success Criteria**: Compliance coverage, security posture, audit results
- **Stakeholders**: Legal, security, compliance officers

## Epic Template Format

**Epic Title**: [Descriptive title reflecting business value]

**Epic Type**: [Strategic/Operational/Technical/Product/Compliance]

**Business Value**: [Clear statement of business impact]

**Success Criteria**:

- [Measurable KPI 1]: [Target value]
- [Measurable KPI 2]: [Target value]
- [Measurable KPI 3]: [Target value]

**Timeline**: [Start date] to [End date] ([X months])

**Stakeholders**:

- **Primary**: [Key decision makers]
- **Secondary**: [Affected teams/users]
- **Communication Plan**: [How stakeholders will be updated]

**Major Features**:

1. **Feature 1**: [Description] - Priority: [High/Medium/Low]
2. **Feature 2**: [Description] - Priority: [High/Medium/Low]
3. **Feature 3**: [Description] - Priority: [High/Medium/Low]

**Risks & Mitigation**:

- **Risk 1**: [Description] - **Mitigation**: [Strategy]
- **Risk 2**: [Description] - **Mitigation**: [Strategy]

## Epic Type Detection Keywords

### Strategic Detection

- "strategic", "business goal", "company objective", "market expansion", "revenue", "growth", "competitive"

### Operational Detection

- "operational", "process", "efficiency", "workflow", "automation", "productivity", "streamline"

### Technical Detection

- "technical", "architecture", "infrastructure", "platform", "scalability", "technical debt", "modernization"

### Product Detection

- "product", "user experience", "customer", "feature", "UX", "user journey", "product roadmap"

### Compliance Detection

- "compliance", "regulatory", "security", "audit", "GDPR", "SOX", "standards", "certification"

## Epic Success Metrics by Type

### Strategic Epic Metrics

- Revenue impact percentage
- Market share growth
- Customer acquisition rate
- ROI (Return on Investment)
- Strategic objective completion rate

### Operational Epic Metrics

- Process efficiency improvement (%)
- Cost reduction achieved ($)
- Time savings per process (hours)
- Error rate reduction (%)
- Process completion rate (%)

### Technical Epic Metrics

- Performance improvement (%)
- Technical debt reduction (%)
- Scalability capacity increase
- Error rate reduction (%)
- System uptime improvement (%)

### Product Epic Metrics

- User satisfaction score (NPS/CSAT)
- Feature adoption rate (%)
- User engagement increase (%)
- Conversion rate improvement (%)
- Customer retention improvement (%)

### Compliance Epic Metrics

- Compliance coverage percentage (%)
- Audit finding reduction (%)
- Security incident reduction (%)
- Certification achievement rate
- Regulatory requirement satisfaction (%)

## Epic Communication Templates

### Stakeholder Updates

**Weekly Status Update Template:**

- Epic Progress: [X% complete]
- Current Milestone: [Milestone name]
- Key Achievements: [3-5 bullet points]
- Challenges & Blockers: [List any issues]
- Next Week Focus: [2-3 priorities]
- Risk Status: [Green/Yellow/Red with details]

### Risk Escalation

**Risk Alert Template:**

- Risk Level: [High/Medium/Low]
- Risk Description: [Clear description]
- Impact Assessment: [Business/technical impact]
- Mitigation Plan: [Specific actions]
- Timeline: [When action needed]
- Escalation Path: [Who needs to be involved]

### Success Celebration

**Milestone Achievement Template:**

- Milestone Completed: [Milestone name]
- Business Value Delivered: [Specific benefits]
- Team Recognition: [Key contributors]
- Lessons Learned: [3-5 insights]
- Next Steps: [What comes next]
