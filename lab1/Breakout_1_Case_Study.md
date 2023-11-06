# Case Study: Setting and Measuring SLIs/SLOs for an Online Bookstore

## Introduction

This workshop focuses on implementing Service Level Indicators (SLIs) and Service Level Objectives (SLOs) for PageTurners, an online bookstore, to boost its reliability and user experience.

If you need a refresher on SLIs and SLOs, check out this [this cheatsheet](./Cheatsheet.md).

## Objectives
- Find out the main steps customers take when using PageTurners.
- Pick the best ways to measure if these steps are working well.
- Decide on good targets for these measurements.

## Scenario

**PageTurners** is a popular online bookstore loved for its wide range of books and easy-to-use website. It has lots of cool features for people who love to read, like previews of books, detailed reviews, suggestions for books you might like, and a smooth way to buy books.

**Features & Things to Think About:**
- **Homepage**: This is like the front door of the bookstore. It should open quickly and show the latest deals and books without any problems.
- **Search**: This helps you find books by their name, author, or type. It should work fast and give you the right results to make you happy.
- **Book Details Page**: This page helps you decide to buy a book and should give you lots of information and previews without making you wait.
- **Buying Books**: The steps to buy a book should be easy and quick, so you can get your book without any trouble.
- **Your Profile**: Here you can see your orders, lists of books you want, and suggestions just for you. It's important that this page is safe and keeps your information correct.
- **Reviews**: Reviews from other readers can help you decide if you want a book. This system should be reliable and show new reviews quickly.
- **Suggestions for You**: The website guesses what books you might like based on what you've looked at or bought before. Good suggestions can help you find more books you'll want to buy.

**Key Performance Numbers:**
1. **When People Visit**: Most people visit the website between 6 PM to 10 PM, so it needs to work best at this time.
2. **Search Speed**: Right now, it takes about 2.3 seconds to see search results.
3. **Buying Quickly**: Data shows that 90% of people finish buying a book within 5 minutes after they choose it.
4. **Reviews Help Sales**: Books with lots of good reviews tend to sell 20% more.
5. **When the Site is Down**: In the past month, the website was not working twice, each time for about 15 minutes. This can make customers trust the website less.

**Stakeholder Interests:**
- **Product Manager**: Focused on overall user satisfaction and how features contribute to the user's journey from discovery to purchase.
- **Web Developer**: Tasked with maintaining a technically robust platform, they are particularly concerned with error rates, latency, and uptime.
- **UX/UI Designer**: Strives to create a design that is both aesthetically pleasing and functionally seamless for the user.
- **Customer Support**: Provides direct feedback on common user issues that can be used to inform improvements in service.
- **Data Analyst**: Utilizes SLIs and SLOs to gather insights into user behavior and platform performance.
- **Marketing Team**: Aims to understand and improve user engagement and conversion rates through the data provided by SLIs and SLOs.

## Part 1 - Identify Critical User Journeys (CUJs)
#### 1.1: Individual task
```Task:``` Identify 3-5 CUJs that exemplify the core experiences on PageTurners.

*Example Answer:*
- Buying a Book: Homepage > Search > Choose Book > Pay

#### 1.2: Group Discussion
```Task:``` Share your critical user paths with your group and discuss which ones are the most important.

## Part 2 - Identify SLIs for each Critical User Journeys (CUJs)
#### 2.1: Individual task
```Task 1:``` For each CUJ you identified in Part 1, identify 2-3 SLIs that effectively measure the user's experience.

```Task 2:``` For each SLI, write a brief description of what the metric measures, why it is important, and an idea for how it will be measured (if you have one).

*Example Answer:*
Measurements for Buying a Book:
- How Long Pages Take to Load: The homepage and search results should show up in 2 seconds.
- How Well Searches Lead to Sales: 95% of the time, when someone searches, they should end up looking at a book's details.

#### 2.2: Group Discussion
```Task:``` Share your SLIs with your group and discuss whether they are the most important ones to measure. 

## Part 3 - Define SLOs for each SLI

#### 3.1: Individual Task
```Task 1:``` For each SLI you identified in Part 2, propose an SLO that represents a target for performance that you believe is attainable, yet aspirational.

When setting SLOs, rememeber to consider the following:
* **Historical Performance:** Look at how the service has performed in the past to set realistic targets.
* **Industry Benchmarks:** Compare against standards in the industry or similar services.
* **Technical Feasibility:** Ensure that the goals are technically possible given current resources and infrastructure.
* **Business Priorities:** SLOs should align with the business's priorities and objectives.
* **Stakeholder Input:** Get feedback from stakeholders to understand what performance levels are necessary for a good user experience.

Assumptions can be made where necessary for this exercise.

```Task 2:``` Write down why you chose each target and how it's a good balance between being challenging and achievable.

*Example Answer:*

Targets for Buying a Book:
- Page Load Time: The homepage and search should load in less than 1.5 seconds for 99% of the time.
- Search to Sale Success: At least 97% of searches should help people go see a book's details.

Reasoning:
- The target for page loading is a bit faster than now to make the website quicker, but it's not too much to ask for. Aiming for 98% means almost everyone will have a fast experience.

- The target for searches leading to sales is higher than the current rate to encourage better search results, helping people find books they're interested in.

#### 3.2: Group Discussion
```Task:``` Talk about the targets you've set with your group. Discuss how they might make things better for the customers and help the bookstore's business.

## Wrapping up 
Debrief as a group if time permits, otherwise, reflect individually post-workshop

1. The importance of data and stakeholder collaboration in setting SLIs and SLOs.
2. How you can apply what you learned to your own organization.
3. The importance of continuously refining SLIs and SLOs based on evolving user needs and technical advancements.

**---STOP HERE - END OF CASE STUDY - THANK YOU FOR PARTICIPATING IN BREAKOUT 1!----**
