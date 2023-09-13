# SLI, SLO, SLA, and Error Budget Cheatsheet

## Definitions

#### SLI (Service Level Indicator)
- Quantitative measure of a service level.
- **E.g.,** The percentage of requests that result in a successful response.

#### SLO (Service Level Objective)
- An internal target level for an SLI over a time period.
- **E.g.,** The successful response rate should be 99.9% over 30 days.

#### SLA (Service Level Agreement)
- Formal agreement with consequences for meeting or missing SLOs. Often listed in contracts and on companies website.
- **E.g.,** If uptime falls below 99.9% in a month, affected users get a credit.

#### Error Budget
- Difference between perfect reliability and the SLO.
- **E.g.,** With a 99.9% SLO, there’s a 0.1% error budget.

## Framework

#### 1. Understand & Define Service
- **Identify Critical User Journeys (CUJs)**: Essential tasks users expect to work.
  - Questions to Ask:
    - What are the most common user operations?
    - Which operations are mission-critical?
  - Stakeholders: Product Managers, End Users, Customer Support Teams.

#### 2. Choose Your SLIs
- Measure what matters to users.
  - Questions to Ask:
    - What metrics reflect user happiness?
    - What is technically measurable?
  - Stakeholders: Engineers, Product Managers, UX Designers.

#### 3. Define Your SLOs
- Set targets stricter than SLAs for a safety margin.
  - Questions to Ask:
    - What level of service do our users expect?
    - What SLOs can we realistically achieve given our current system and resources?
  - Stakeholders: Business Leaders, Engineers, Product Managers.

#### 4. Formalize Your SLAs
- Define consequences if SLOs aren't met.
  - Questions to Ask:
    - What are appropriate penalties or compensations for not meeting SLOs?
    - How will we communicate breaches in SLOs to users?
  - Stakeholders: Legal Team, Business Leaders, Customer Relations.

#### 5. Calculate & Monitor Error Budgets
- Allows balancing between innovation and reliability.
  - Questions to Ask:
    - How will we track and report on our error budget consumption?
    - What corrective actions will we take if we exceed our error budget?
  - Stakeholders: Engineers, SRE Team, Product Managers.

#### 6. Adjust Based on Learnings
- Make iterative improvements.
  - Questions to Ask:
    - What did we learn from our last error budget period?
    - Are our SLOs still aligned with business objectives and user needs?
  - Stakeholders: Engineers, SRE Team, Product Managers, Business Analysts.

#### 7. Communication
- Ensure everyone understands and is aligned on SLIs, SLOs, and SLAs.
  - Questions to Ask:
    - How will we educate our team about these concepts?
    - How will we inform users about our service levels and any changes?
  - Stakeholders: All Teams, especially Communication/PR and Customer Support.