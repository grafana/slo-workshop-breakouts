# Case Study: Setting and Measuring SLIs/SLOs for an Online Bookstore

## Introduction

In today's digital world, it's essential to ensure that users have a seamless experience. Organizations use Service Level Indicators (SLIs) and Service Level Objectives (SLOs) to measure and improve this experience. This case study will take you deep into the world of PageTurners, an online bookstore, to show you how to implement these concepts.

If you need a refresher on SLIs, SLOs, SLAs, and Error Budgets, check out this [this cheatsheet](./Cheatsheet.md).

## Objectives
- Understand the intricacies of setting SLIs and determining SLOs.
- Recognize the importance of data and stakeholder collaboration.
- Be equipped to start implementing SLIs/SLOs in your organizations.

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

## Part 1 [Individual Task] - Identify Critical User Journeys (CUJs)

```Task:``` Based on the provided background, list 3-5 critical user journeys (CUJs) that are vital for PageTurners. Then rank them based on their significance to user satisfaction and potential revenue impact (ie Very High, High, Medium, Low).

```Fillout:```
| Critical User Journeys (CUJs) | Significance to User Satisfaction | Potential Revenue Impact | Priority |
|----------|----------|----------|----------|
| Browsing and searching for books  | Very High  | Medium  | High |
| _ | _ | _ | _ |
| _ | _ | _ | _ |
| _ | _ | _ | _ |
| _ | _ | _ | _ |
| _ | _ | _ | _ |

## Part 2 [Instructor Led] - Group Discussion on Critical User Journeys (CUJs)

```Task:``` Share items off of your individual critical user journey (CUJ) list. Work together to refine and finalize a priority list, making sure that we have a complete understanding of user needs.

## Part 3 [Individual Task] - Determine potential on SLIs Using Key Stats

```Task:``` Determine potential SLIs (service level indicators) for each critical user journey (CUJ), using the provided key stats. For critical user journey (CUJ) without direct data from the key stats, identify stakeholders who can provide insights.

```Hint:```
| Method |	Example SLIs |
|----------|----------|
| RED	| Search result load time, error rate, search query throughput |
| 4 golden signals | Latency, traffic, errors, saturation |

```Fillout:```
| Critical User Journeys (CUJs) (CUJ) | Potential SLIs | Why | Key stats used | Stakeholders to consult |
|----------|----------|----------|----------|----------|
| Search for a product | Search results should appear within 2.5 seconds | To ensure that users can quickly find the products they are looking for, which improves the user experience and increases the likelihood of a purchase. | Average search result load time | Engineers |
| _ | _ | _ | _ | _ |
| _ | _ | _ | _ | _ |
| _ | _ | _ | _ | _ |
| _ | _ | _ | _ | _ |

## Part 4 [Instructor Led] - Group Discussion on SLIs

```Task:``` Share individual SLIs determined from the key stats. Collaboratively discuss, ensuring they're measurable, relevant, and aligned with user expectations.

## Part 5 [Instructor Led] - Group Discussion on Data Requirements & Stakeholders for Setting SLOs

```Task:``` Discuss what additional data might be essential for each SLI to set a realistic SLO. Then identify which stakeholders would provide this data or offer insights into setting these SLOs.

## Wrapping up 

Debrief as a group if time permits, otherwise, reflect individually post-workshop

1. The importance of data and stakeholder collaboration in setting SLIs and SLOs.
2. How you can apply what you learned to your own organization.
3. The importance of continuously refining SLIs and SLOs based on evolving user needs and technical advancements.

**---STOP HERE - END OF CASE STUDY - THANK YOU FOR PARTICIPATING IN BREAKOUT 1!----**