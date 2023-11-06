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

#### Critical User Journeys (CUJs)
- Essential user interactions with a product or service that are vital to achieving both user satisfaction and business objectives. CUJs are identified by examining:
    * User Goals - The primary objectives or tasks that users aim to accomplish using the product or service.
    * User Pain Points - The hurdles or obstacles users encounter that impede their progress toward reaching their goals.
    * Business Outcomes - The key results or achievements that the business aims to realize, which are often directly influenced by user success in completing these journeys.
- **E.g.,** For an e-commerce platform, a CUJ might be the end-to-end process of searching for a product, adding it to the cart, and completing the checkout process seamlessly.

## Benefits of Setting SLIs and SLOs
#### Why is it important to set SLIs and SLOs?

- Ensure that our services are meeting the needs of our users.
- Identify and address potential problems with our services before they impact our users.
- Communicate the performance of our services to stakeholders.

#### What are some challenges in setting SLIs and SLOs?

- Choosing the right metrics to measure.
- Setting realistic and achievable targets.
- Gathering the data needed to measure SLIs.
- Getting buy-in from stakeholders.

#### How can data and stakeholder collaboration help us set realistic and achievable SLIs and SLOs?

- Helping us to identify the most important metrics to measure.
- Helping us to understand the current performance of our services.
- Helping us to identify and address potential bottlenecks and constraints.
- Helping us to set targets that are aligned with the needs of our users and stakeholders.

#### What are some best practices for continuously refining SLIs and SLOs based on evolving user needs and technical advancements?

- Regularly review SLIs and SLOs to ensure that they are still relevant and aligned with user needs and technical advancements.
- Use data to track progress towards SLOs and identify areas for improvement.
- Collaborate with stakeholders to get their input on refining SLIs and SLOs.

## Framework for Setting SLIs, SLOs, SLAs, and Error Budgets
#### 1. Identify stakeholders.

The stakeholders should be involved in the process from start to finish, so it's important to identify them early on.

*Considerations:*
- Who will be impacted by the SLIs, SLOs, SLAs, and error budgets?
- Who has the knowledge and expertise to contribute to the process?
- How can we ensure that all relevant stakeholders are represented?

*Potential Stakeholders:*
Product managers, end users, customer support teams, engineers, product managers, UX designers, business leaders, legal team, business leaders, customer relations, SRE team, business analysts, communication/PR team

#### 2. Understand & define service.

The more you understand about your service and its users, the better equipped you will be to set realistic and achievable SLIs, SLOs, SLAs, and error budgets.

*Considerations:*
- What are the critical user journeys (CUJs)?
- What are the user expectations for each CUJ?
- What are the key components of the service that support each CUJ?
- What are the dependencies between different components of the service?
- What are the known failure modes of the service?

*Potential Stakeholders:* 
Product managers, end users, customer support teams

#### 3. Choose your SLIs.

SLIs should be measurable, relevant, and actionable.

*Things to think about:*
- What metrics reflect user happiness and are technically measurable?
- What are the most important aspects of the service to measure?
- How can we ensure that we have a representative set of SLIs that cover all aspects of the service?
- How will we collect and aggregate the data needed to measure the SLIs?

*Potential Stakeholders:* 
Engineers, product managers, UX designers

#### 4. Define your SLOs.

SLOs should be ambitious but achievable.

*Considerations:*
- What level of service do our users expect? If you have a SLA with your customers, your SLOs should meet or exceed the SLA requirements.
- What SLOs can we realistically achieve given our current system and resources?
- How can we balance the need for reliability with the need for innovation?
- How will we measure and report on SLO compliance?

*Potential Stakeholders:*
Business leaders, engineers, product managers

#### 5. Formalize your SLAs.

SLAs should be clear, concise, and enforceable.

*Considerations:*
- What are the appropriate consequences for meeting or missing SLOs?
- How will we communicate the SLAs to users and stakeholders?
- How will we measure and report on SLA compliance?
- How will we handle customer complaints and disputes?

*Potential Stakeholders:*
Legal team, business leaders, customer relations

#### 6. Calculate & monitor error budgets.

Error budgets should be calculated based on the SLOs and the tolerance for risk.

*Considerations:*
How much error budget should we allocate to each SLI?
How will we track and report on error budget consumption?
What corrective actions will we take if we exceed our error budget?
How will we communicate any changes in error budget to users and stakeholders?

*Potential Stakeholders:*
Engineers, SRE team, product managers

#### 7. Review & iterate.

SLIs, SLOs, SLAs, and error budgets should be reviewed and iterated on regularly to ensure that they are still aligned with business objectives and user needs.

*Considerations:*
- Are our SLIs, SLOs, SLAs, and error budgets still aligned with business objectives and user needs?
- What lessons have we learned from our previous error budget period?
- How can we improve our SLIs, SLOs, SLAs, and error budgets over time?

*Potential Stakeholders:* 
Engineers, SRE team, product managers, business analysts
