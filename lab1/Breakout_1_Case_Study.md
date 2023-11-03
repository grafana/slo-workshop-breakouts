# Case Study: Setting and Measuring SLIs/SLOs for an Online Bookstore

## Introduction

In today's digital world, it's essential to ensure that users have a seamless experience. Organizations use Service Level Indicators (SLIs) and Service Level Objectives (SLOs) to measure and improve this experience. This case study will take you deep into the world of PageTurners, an online bookstore, to show you how to implement these concepts.

If you need a refresher on SLIs, SLOs, SLAs, and Error Budgets, check out this [this cheatsheet](./Cheatsheet.md).

## Objectives
1. Understand the intricacies of setting SLIs and determining SLOs.
2. Recognize the importance of data and stakeholder collaboration.
3. Be equipped to start implementing SLIs/SLOs in your organizations.

## Scenario

**PageTurners** is a thriving online bookstore with a wide selection of books. Their platform includes features such as book previews, user reviews, personalized recommendations, and checkout.

**Website Features:**
- Homepage - The face of the business, it must load quickly and without errors.
- Search Functionality - Essential for users to quickly find their desired books.
- Book Details Page - A deciding factor for purchases, it must be detailed and responsive.
- Checkout Process - Directly tied to revenue, it must be seamless.
- User Profile - Personal space for users, privacy and accuracy are paramount.
- Review System - Influences purchasing decisions, it should be genuine and timely.
- Recommendation Engine - Drives sales through suggestions, accuracy is crucial.

**Roles within PageTurners & Their Stake in SLIs/SLOs:**
- Product Manager - Concerned with overall user satisfaction.
- Web Developer - Ensures technical robustness, keen on error rates and latency.
- UX/UI Designer - Wants to ensure design translates to functionality.
- Customer Support - Has data on common user issues.
- Data Analyst - Uses SLIs/SLOs for insights on user behavior.
- Marketing Team - Interested in user engagement and conversion rates.

**Key Stats:**
1. User Behavior - 70% of users visit the site between 6 PM to 10 PM, indicating peak hours.
2. Search Functionality - On average, search results load in 2.3 seconds.
3. Checkout Process - 90% of users complete their purchase within 5 minutes of adding a book to the cart.
4. User Reviews - There's a 20% increase in book sales with more than 50 positive reviews.
5. Site Downtime - The site has experienced downtime twice in the past month, lasting about 15 minutes.

## Task 1: Identify Critical User Journeys (CUJs) - Individual Assignment

Based on the provided background, list 3-5 customer user journeys (CUJs) that are vital for PageTurners. Then rank them based on their significance to user satisfaction and potential revenue impact (ie Very High, High, Medium, Low).

| Customer User Journey (CUJs) | Significance to User Satisfaction | Potential Revenue Impact | Priority |
|----------|----------|----------|----------|
| Browsing and searching for books  | Very High  | Medium  | High |
| -  | -  | -  | -  |
| -  | -  | -  | -  |
| -  | -  | -  | -  |
| -  | -  | -  | -  |

## Task 2: Group Discussion on CUJs - Instructor Led

Share your individual customer user journey (CUJ) lists. Work together to refine and finalize a priority list, making sure that we have a complete understanding of user needs.

## Task 3: Determine potential on SLIs Using Key Stats - Individual Assignment

Determine potential SLIs (service level indicators) for each customer user journey (CUJ), using the provided key stats. For CUJs without direct data from the key stats, identify stakeholders who can provide insights.
   *Example: "Given that search results currently load in 2.3 seconds on average, an SLI could be that search results should appear within 2.5 seconds."*

   *Example: "To understand the expected conversion rate for the checkout process, I would consult with the product manager and marketing team."*

## Task 4: Group Discussion on SLIs - Instructor Led

Share individual SLIs determined from the key stats. Collaboratively discuss, ensuring they're measurable, relevant, and aligned with user expectations.

## Task 5: Data Requirements & Stakeholder Consultation for Setting SLOs - Instructor Led

Discuss what additional data might be essential for each SLI to set a realistic SLO.
   *Example: To set a realistic SLO for our 2.5-second search result SLI, we need to know the load time during peak hours.*

Then identify which stakeholders would provide this data or offer insights into setting these SLOs.
   *Example: "The Web Developer might have data on site performance during high traffic times."*

## Wrapping up 

*Debrief as a group if time permits, otherwise, reflect individually post-workshop*

1. The importance of data and stakeholder collaboration in setting SLIs and SLOs.
2. How you can apply what you learned to your own organization.
3. The importance of continuously refining SLIs and SLOs based on evolving user needs and technical advancements.

**---STOP HERE - END OF CASE STUDY - THANK YOU FOR PARTICIPATING IN BREAKOUT 1!----**