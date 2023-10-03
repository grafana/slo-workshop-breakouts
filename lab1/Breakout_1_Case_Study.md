# Case Study: Setting and Measuring SLIs/SLOs for an Online Bookstore

## Introduction

In today's digital age, ensuring a seamless user experience is paramount. Service Level Indicators (SLIs) and Service Level Objectives (SLOs) are tools that organizations use to quantify and improve this experience. Through this case study, you will delve deep into the world of PageTurners, an online bookstore, to understand and implement these concepts.

Checkout [this cheatsheet](./Cheatsheet.md) if you need a refresher on SLIs, SLOs, SLAs, and Error Budgets.

## Expected Outcomes
1. Understand the intricacies of setting SLIs and determining SLOs.
2. Recognize the importance of data and stakeholder collaboration.
3. Be equipped to start implementing SLIs/SLOs in your organizations.

## Background

**PageTurners** is a bustling online bookstore with a diverse range of books. Their platform has features such as book previews, user reviews, personalized recommendations, and an e-reader interface.

### Website Features:
1. **Homepage:** The face of the business; it must load quickly and without errors.
2. **Search Functionality:** Crucial for users to find their desired books efficiently.
3. **Book Details Page:** A deciding factor for purchases; needs to be detailed and responsive.
4. **Checkout Process:** Directly tied to revenue; must be seamless.
5. **User Profile:** Personal space for users; privacy and accuracy are paramount.
6. **E-reader Interface:** For digital readers; functionality and speed are key.
7. **Review System:** Influences purchasing decisions; should be genuine and timely.
8. **Recommendation Engine:** Drives sales through suggestions; accuracy is crucial.

### Roles within PageTurners & Their Stake in SLIs/SLOs:
1. **Product Manager:** Concerned with overall user satisfaction.
2. **Web Developer:** Ensures technical robustness; keen on error rates and latency.
3. **UX/UI Designer:** Wants to ensure design translates to functionality.
4. **Customer Support:** Has data on common user issues.
5. **Data Analyst:** Uses SLIs/SLOs for insights on user behavior.
6. **Marketing Team:** Interested in user engagement and conversion rates.

### Key Stats:
1. **User Behavior:** 70% of users visit the site between 6 PM to 10 PM, indicating peak hours.
2. **Search Functionality:** On average, search results load in 2.3 seconds.
3. **Checkout Process:** 90% of users complete their purchase within 5 minutes of adding a book to the cart.
4. **User Reviews:** There's a 20% increase in book sales with more than 50 positive reviews.
5. **E-reader Interface:** 80% of users switch between reading and listening at least once during a session.
6. **Site Downtime:** The site has experienced downtime twice in the past month, lasting about 15 minutes.

### Task 1: Identify Critical User Journeys (CUJs)

**Instructions:**
1. Based on the provided background, individually list 3-5 CUJs you believe are vital for PageTurners.
   *Example: A user searching for a book, reading reviews, and making a purchase.*
2. Rank them based on their significance to user satisfaction and potential revenue impact.

## Task 2: Group Discussion on CUJs

**Instructions:**
1. Share individual CUJ lists.
2. Collaboratively refine and finalize a priority list, ensuring a holistic understanding of user needs.

## Task 3: Individual Assignment on SLIs Using Key Stats

**Instructions:**
1. Using the provided key stats, determine potential SLIs for each CUJ.
   *Example: "Given that search results currently load in 2.3 seconds on average, an SLI could be that search results should appear within 2.5 seconds."*
2. For CUJs without direct data from the key stats, consider which stakeholders you'd consult for insights.
   *Example: "To understand the expected responsiveness of the e-reader interface, I'd approach the UX/UI Designer and Web Developer."*

## Task 4: Group Discussion on SLIs

**Instructions:**
1. Share individual SLIs determined from the key stats.
2. Collaboratively discuss, ensuring they're measurable, relevant, and aligned with user expectations.

## Task 5: Data Requirements & Stakeholder Consultation for Setting SLOs

**Instructions**
1. Discuss what additional data might be essential for each SLI to set a realistic SLO.
   *Example: "For our 2.5-second search result SLI, what's the load time during peak hours?"*
2. Identify which stakeholders would provide this data or offer insights into setting these SLOs.
   *Example: "The Web Developer might have data on site performance during high traffic times."*

## Wrapping up the Case Study 

**Instructions:** *Debrief as a group if time permits, otherwise, reflect individually post-workshop*
1. The importance of data and stakeholder collaboration in setting SLIs and SLOs.
2. How this exercise can be mirrored in your own organizations.
3. The continuous nature of refining SLIs/SLOs based on evolving user needs and technical advancements.

## ---End of Case Study----
Thank you for participating!
