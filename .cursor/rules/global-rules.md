# Global Rules for User Story Creation and Validation

## User Story Format

```gherkin
As a [role/persona]
I want [capability/feature]
So that [benefit/value]
```

## INVEST Principles Checklist
Each story MUST conform to:
- **Independent**: Can be delivered separately from other stories
- **Negotiable**: Room for discussion about implementation
- **Valuable**: Delivers clear value to a stakeholder
- **Estimable**: Team can estimate the effort required
- **Small**: Completable within one sprint
- **Testable**: Has clear acceptance criteria

## Acceptance Criteria Requirements
- Must use Gherkin syntax:

```gherkin
Given [initial context/precondition]
When [action/event occurs]
Then [expected outcome]
```

- At least one scenario per story
- Cover happy path and key error paths
- No technical implementation details
- Measurable and verifiable outcomes

## Foundation Sprint (Sprint 0) Requirements
Stories in Sprint 0 must focus on:

### Core Foundation Elements
1. **Data Foundation**
   - Complete initial data model
   - Define key entities and relationships
   - Establish data governance rules
   - Document data security requirements
   - Define data retention policies

2. **User Personas**
   - Define primary user personas
   - Document user roles and permissions
   - Establish user journeys
   - Define accessibility requirements
   - Document user security contexts

### Technical Foundation
3. **Environment Setup**
   - Development environment
   - Testing environment
   - CI/CD pipeline basics
   - Monitoring setup

4. **Architecture Foundation**
   - System architecture
   - Integration points
   - Security architecture
   - Performance requirements

5. **Development Standards**
   - Coding standards
   - Testing standards
   - Documentation requirements
   - Security standards

### Sprint 0 Definition of Done
- [ ] Data model approved by technical team
- [ ] User personas validated by stakeholders
- [ ] Environment access configured for team
- [ ] Security requirements documented
- [ ] Architecture decisions documented

### Sprint 0 Risk Assessment
The Agile PM/Scrum Master MUST conduct a formal risk assessment at the end of Sprint 0. Any incomplete foundational elements represent critical project risks and must be:

1. **Documented and Escalated**
   - Risk added to project risk register
   - Immediate escalation to project sponsors
   - Impact assessment on subsequent sprints
   - Mitigation plan developed

2. **Foundational Elements Risk Levels**
   - **HIGH RISK**: Incomplete Data Model or User Personas
   - **HIGH RISK**: Missing Security Requirements
   - **MEDIUM RISK**: Incomplete Environment Setup
   - **MEDIUM RISK**: Incomplete Architecture Decisions
   - **MEDIUM RISK**: Missing Development Standards

3. **Required Actions**
   - Schedule immediate remediation sprint
   - Add stories to address gaps in Sprint 1
   - Document technical debt items
   - Create dependency map for affected future stories

4. **Risk Acceptance Criteria**
   - Project sponsor sign-off required for proceeding with known gaps
   - Written acknowledgment of impact on project timeline
   - Documented plan for addressing gaps
   - Clear ownership of remediation actions

### Impact on Future Stories
Stories in subsequent sprints that depend on incomplete foundational elements must:
- Include additional acceptance criteria addressing the gap
- Be flagged as "AT RISK" in the backlog
- Have explicit dependencies documented
- Include temporary workarounds where applicable

## Story Sizing Guidelines
- XS: 1-2 days
- S: 3-5 days
- M: 5-8 days
- L: Must be broken down further

## Definition of Ready
- [ ] Follows story format
- [ ] Meets INVEST criteria
- [ ] Has Gherkin acceptance criteria
- [ ] Estimated by team
- [ ] Dependencies identified
- [ ] Risks documented

## Example Story - Standard Implementation

```gherkin
Title: Configure Single Sign-On for New Starter Portal

As a new employee
I want to use my corporate credentials to access the starter portal
So that I can securely access my onboarding materials without managing multiple logins

Acceptance Criteria:

Scenario: Successful SSO Login
Given I am a new employee with active corporate credentials
When I visit the starter portal
Then I should be automatically authenticated using my corporate account
And I should see my personalized onboarding dashboard

Scenario: Invalid Corporate Credentials
Given I am a user with inactive corporate credentials
When I attempt to access the starter portal
Then I should see an error message directing me to contact IT Support
And I should not gain access to the portal

Size: S (3-5 days)
Dependencies: Active Directory integration
Risks: SSO provider availability
```

## Example Story - With Foundational Gap

```gherkin
Title: Create User Profile for New Employee

As a new employee
I want to set up my user profile
So that I can access personalized onboarding content

Note: AT RISK - Incomplete Data Model Foundation
Related Risk: RISK-2023-001 (Data Model Gap - User Preferences Schema)

Acceptance Criteria:

Scenario: Basic Profile Creation (Temporary Implementation)
Given I am a new employee with active credentials
When I create my profile
Then only my essential details should be stored (name, department, role)
And a technical debt ticket should be created for migration when full schema is ready
And my profile should be flagged for update once data model is complete

Scenario: Profile Update After Data Model Completion
Given the complete user preference schema is implemented
When the migration script runs
Then my profile should be prompted for additional information
And no user data should be lost during migration

Technical Dependencies:
- Temporary data storage solution approved by architecture team
- Migration strategy documented and approved
- Monitoring for data consistency during transition

Mitigation Approach:
- Using simplified schema with extension capability
- Implementing feature flags for gradual enhancement
- Maintaining data export capability for future migration

Size: M (5-8 days) - Includes temporary solution overhead
Original Estimate without Gap: S (3-5 days)
Additional Complexity: Migration planning and temporary schema
```

## Risk Documentation Template

```markdown
Risk ID: RISK-[YEAR]-[NUMBER]
Title: [Clear, specific title]
Category: Foundation Gap
Impact Level: [HIGH|MEDIUM|LOW]

Foundation Element Affected:
- [ ] Data Model
- [ ] User Personas
- [ ] Security Requirements
- [ ] Environment Setup
- [ ] Architecture Decisions
- [ ] Development Standards

Impact Assessment:
1. Immediate Impact:
   - [List immediate effects on current sprint]
   - [List affected stories/features]

2. Future Impact:
   - [List affected future sprints/features]
   - [Estimate of additional effort/complexity]

3. Technical Debt:
   - [List technical debt items created]
   - [Estimate remediation effort]

Mitigation Plan:
1. Short-term Actions:
   - [List immediate actions]
   - Owner: [Name]
   - Timeline: [Date]

2. Long-term Resolution:
   - [List permanent solution steps]
   - Owner: [Name]
   - Target Completion: [Date]

Sign-off Requirements:
- [ ] Technical Lead Review
- [ ] Architecture Review
- [ ] Product Owner Acknowledgment
- [ ] Project Sponsor Approval

Status Updates:
| Date | Update | Owner |
|------|---------|-------|
| [Date] | [Description] | [Name] |
```

## Azure DevOps Implementation

### Risk and Decision Tracking in ADO
1. **Work Item Configuration**
   - Add tag "AT-RISK" to affected stories
   - Add tag "DECISION-REQUIRED" when story needs architectural/technical decision
   - Use custom fields:
     - "Risk Reference" to link to risk register
     - "Decision Reference" to link to decision log
   - Include wiki links in description:
     - Risks: `[Risk Details](wiki/project-governance/risk-register#risk-id)`
     - Decisions: `[Decision Details](wiki/project-governance/decision-log#decision-id)`

2. **Documentation Location**
   - Risk Register maintained in project Wiki (`wiki/project-governance/risk-register.md`)
   - Decision Log maintained in project Wiki (`wiki/project-governance/decision-log.md`)
   - Update during sprint ceremonies

3. **Required Links**
   - Stories must link to related risks and decisions
   - Risk/Decision logs must link to affected stories
   - All links must be bi-directional

4. **Visibility**
   - Use ADO queries to track items needing decisions
   - Include risk/decision status in sprint reviews
   - Maintain dashboard for stakeholder visibility

### Story Requirements for Decisions
Stories that implement significant decisions must:
- Reference the decision ID in the story
- Include decision-specific acceptance criteria
- Link to the decision in the wiki
- Be reviewed against decision requirements
- Include any temporary/migration steps if needed

### Risk Tracking in ADO
1. **Work Item Configuration**
   - Add tag "AT-RISK" to affected stories
   - Use custom field "Risk Reference" to link to risk register
   - Include wiki link in description: `[Risk Details](wiki/project-governance/risk-register#risk-id)`

2. **Risk Register Location**
   - Maintained in project Wiki
   - Follow template in `project-risk-register.md`
   - Update weekly during sprint ceremonies

3. **Required Links**
   - Each AT-RISK story must link to Wiki risk register
   - Risk register must link to affected stories
   - All links must be bi-directional

4. **Visibility**
   - Use ADO queries to track at-risk items
   - Include risk status in sprint reviews
   - Maintain risk dashboard for stakeholders 