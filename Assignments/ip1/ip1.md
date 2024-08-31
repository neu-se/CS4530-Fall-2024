---
layout: assignment
title: "Individual Project 1"
permalink: /assignments/ip1
parent: Assignments
nav_order: 1
due_date: "Wednesday September 18, 2024 12:00pm EST (Noon)"
submission_notes: TBA
---

Welcome aboard to the Stack Overflow team! We're glad that you're here and ready to join our development team as a new software engineer.
We're building an interactive application for online community to share their knowledge and experience, and are very happy to see that we have so many new developers who can help make this application a reality.
By the end of the semester, you'll be able to propose, design, implement and test a new features for our project.
We understand that some of you may have some web development experience, but don't expect that most of you do, and hence, have created an individual project to help you get up to speed with our existing codebase and development environment.

FakeStackOverFlow is a web application that consists of some code that runs in each client's web browser, and also code that runs on a server.
**TOUPDATE:** Users join the application in a "town": a 2D arcade-style map with different rooms to explore.
Each town is also a video call: when two players get close to each other, they can see and hear each other; there is also a text chat available within the town.
In Winter of 2021, our lead software engineer, Avery, developed a prototype for Covey.Town, and since then, hundreds of students in this class have built on that codebase.
The most recent class-wide effort, in Fall 2023, added a concept called [Game Areas](https://neu-se.github.io/CS4530-Fall-2023/assignments/ip1), allowing players to play games within a special part of the town. 
Students implemented a single game, [Tic-Tac-Toe](https://en.wikipedia.org/wiki/Tic-tac-toe), as a proof-of-concept for this feature.

The objective for this semester's individual project is to **TOUPDATE**.
This implementation effort will be split across two deliverables. In this first deliverable, you will implement and test the core backend components for this feature, and in the second deliverable, you will implement and test the frontend components. 

## Objectives of this assignment
The objectives of this assignment are to:
*  Get you familiar with the basics of TypeScript, VSCode, and the project codebase
*  Learn how to read and write code in TypeScript
*  Translate high-level requirements into code
*  Learn how to write unit tests with Jest

## Getting started with this assignment

Before you begin, be sure to check that you have NodeJS 18.x installed, along with VSCode. We have provided a tutorial on setting up a development environment for this class. 
Start by downloading the [starter code]({{site.baseurl}}{% link /Assignments/ip1/ip1_starter_code.zip %}). Extract the archive and follow the instructions given in readme.md file to configure the server and client. **Please extract the entire archive** instead of copying files over. Avery has also provided you with some very basic sanity tests that you can extend for testing your implementation as you go.


## Submission Instructions & Grading
You will submit your assignment via GitHub Classroom.

To submit your assignment: run the command `npm run zip` in the top-level directory of the handout. 

This submission will be scored out of 100 points, 90 of which will be awarded for implementation of tasks and accompanying tests, and the remaining 10 for following style guidelines.

* Testing
You will be provided with starter code that includes a set of tests. Your task is to ensure that all existing tests pass and to create additional tests to cover any new functionality or edge cases.

Your code will be evaluated for linter errors and warnings. Submissions that have *any* linter errors will automatically receive a grade of 0. **Do not wait to run the linter until the last minute**. To check for linter errors, run the command `npm run lint` from the terminal. The handout contains the same eslint configuration that is used by our grading script.

* Manual Grading
Your code will be manually evaluated for conformance to our course style guide. This manual evaluation will account for 10% of your total grade on this assignment. We will manually evaluate your code for style on the following rubric:

To receive all 10 points:
* All new names (e.g. for local variables, methods, and properties) follow the naming conventions defined in our style guide
* There are no unused local variables
* All public properties and methods (other than getters, setters, and constructors) are documented with JSDoc-style comments that describes what the property/method does, as defined in our style guide
* The code and tests that you write generally follows the design principles discussed in week one. In particular, your design does not have duplicated code that could have been refactored into a shared method.


We will review your code and note each violation of this rubric. We will deduct two points for each violation, up to a maximum of deducting all 10 style points.

* Debugging : 
If you need help troubleshooting a problem, be sure to follow all the steps outlined in the course's debugging policy. This will ensure that you've exhausted all initial debugging strategies before reaching out for assistance from TAs.

## Implementation Tasks
This deliverable has four parts; each part will be graded on its own rubric. You should complete the assignment one part at a time, in the order presented here.

### Task 1: Implement Filtering by asked_by Field
The `asked_by` field in the questions schema represents the username of the user who asked the question, essentially identifying the author of the question. The objective of this task is to enhance the current functionality by adding the capability to filter questions based on the `asked_by` field. This will allow users to retrieve questions posted by a specific user.

#### Steps to Achieve This
1. Add the filterQuestionsByAskedBy Function
Create a new function called `filterQuestionsByAskedBy` in the `application.ts` file. This function will accept a list of questions and the name of a user as arguments and filter the given list of questions, returning only those asked by the specified user.
2. Update the getQuestionsByFilter Function
Modify the `getQuestionsByFilter` function within the questions controller to incorporate the new filtering functionality based on the `asked_by` field. This involves integrating the `filterQuestionsByAskedBy` function to ensure that the questions are filtered by the specified user before any other filtering operations.
3. Testing the Implementation
After implementing these changes, it's crucial to thoroughly test the new functionality. Ensure that questions are correctly filtered by the `asked_by` field, and that the existing filtering mechanisms (by search keywords and tags) remain unaffected. To demonstrate your understanding, add tests to `application.spec.ts`.

Grading for implementation tasks:
* Adding `filterQuestionsByAskedBy`: 5 points
* Updating `getQuestionsByFilter`: 5 points
* Testing: 3 points

### Task 2: Enhancing the Tags Model by Adding a Description Field
The goal of this task is to enhance the existing Tags model by introducing a description field. This new field will allow users to have a descriptive overview of each tag, improving the user experience when interacting with tags. The following steps outline the modifications required in the server to accommodate this new field.

#### Steps to Achieve This
1. Update the `getTags` Function
The current `getTags` function in `application.ts` accepts an array of tag names as strings. This function needs to be modified to accept mock tag objects from the client, which will include both the tag name and description. The updated function will:
* Remove duplicate tags.
* Check the database for existing tags.
* Create new tags if they do not already exist.
* Return the modified tags to be added to the questions.

2. Add the `getTagByName` endpoint to tags controller. 
To allow the client to display tags along with their descriptions, a new endpoint, `getTagByName`, will be added to the tags controller. This endpoint will:
* Accept a tag’s unique name as input.
* Return the corresponding tag, including its name and description

3. Testing the Implementation
To ensure the new feature works correctly, the following tests will be conducted:
* Unit Testing: Verify that the `getTags` function correctly handles the creation of new tags, removal of duplicates, and retrieval of existing tags.
* Endpoint Testing: Test the `getTagByName` endpoint to ensure it accurately returns the correct tag data based on the provided name.
* Integration Testing: Validate the interaction between the updated `getTags` function and the `addQuestion` endpoint to ensure the entire process of tag 
retrieval and creation functions smoothly.

Grading for implementation tasks:
* Update `getTags`: 4 points
* Add `getTagByName`: 4 points
* Testing: 2 points

### Task 3: Implement Sorting by Most Views
As part of this task, you will be working on a function to retrieve questions based on their view count. You are provided with the `getQuestionsByOrder` function which is currently designed to fetch questions from a database and sort them based on the specified order. The function currently supports fetching active, unanswered, and newest questions. Your task is to implement the logic for fetching the most viewed questions.

#### Steps to Achieve This
1. Update the OrderType type
Update the existing data type `OrderType` in the `types.ts` file to support the feature you are going to implement.

2. Add the getMostViewedQuestion Function
Create a new function called `getMostViewedQuestion` in the `application.ts` file. This function should take a list of questions as input and return the questions sorted by their view count in descending order.

3. Update the getQuestionsByOrder Function
Modify the `getQuestionsByOrder` function within the same file (`application.ts`) to incorporate the new sorting functionality. This involves integrating the changes made to the data type in Step 1 and utilizing the function implemented in Step 2.

4. Testing the Implementation
After implementing these changes, it's crucial to thoroughly test the new functionality. Ensure that questions are correctly sorted by most views, and that the existing sorting features (active, unanswered and newest) remain unaffected. To demonstrate your understanding, add tests to `application.spec.ts`.

Grading for implementation tasks:
* Update OrderType: 3 points
* Add `getMostViewedQuestion`: 5 points
* Update `getQuestionsByOrder`: 3 points
* Testing: 2 points

### Task 4: Implement Upvoting and Downvoting Functionality
The upvoting and downvoting features allow users to express their opinions on questions by adding or removing their votes. This functionality is crucial for a community-driven platform where user engagement and feedback are important.

#### Upvoting a Question
When a user upvotes a question, the following actions take place:
* **Update Upvotes List:** The user's username is added to the `up_votes` field of the question. This field is an array that tracks all the users who have upvoted the question.
* **Remove Downvote (if present):** If the user had previously downvoted the question, their username is removed from the `down_votes` list to prevent contradictory actions by the same user.
* **Success and Cancellation:** If the user has already upvoted the question, their vote can be cancelled, which involves removing their username from the `up_votes` list.

#### Downvoting a Question
Similarly, when a user downvotes a question:
* **Update Downvotes List:** The user's username is added to the `down_votes` field of the question. This field is an array that records all the users who have downvoted the question.
* **Remove Upvote (if present):** If the user had previously upvoted the question, their username is removed from the `up_votes` list.
* **Success and Cancellation:** If the user has already downvoted the question, their vote can be cancelled, which involves removing their username from the `down_votes` list.

#### Key Points
* Each question maintains two separate lists: `up_votes` and `down_votes`, which are updated based on user interactions.
* Users can toggle their vote on a question, which means they can switch from upvoting to downvoting or vice versa.
* Proper error handling ensures that issues like missing fields in requests or database errors are managed appropriately, providing a smooth user experience.

#### Steps to Achieve This
1. Add Upvote and Downvote Functions
Implement two functions `addUpvoteToQuestion` and `addDownvoteToQuestion` in `server/models/application.ts` to handle upvoting and downvoting of questions. These functions will:
* Check if the question exists.
* Add or remove the user's vote (upvote or downvote) as appropriate.
* Update the question’s upvote and downvote counts.

2. Update Routes to Handle Voting
Add two new routes `"/upvoteQuestion"` and `"/downvoteQuestion"` in `server/controller/question.ts` to handle upvote and downvote requests. These routes will use the newly created functions to update the question's votes.

3. Test the Voting Functionality
Write tests in tests/question.spec.ts to verify the behavior of the upvote and downvote features. The tests should cover:
* Successful upvoting and downvoting.
* Cancelling an upvote or downvote.
* Handling edge cases such as missing parameters in requests.

Grading for implementation tasks:
* `addUpvoteToQuestion` and `addDownvoteToQuestion`: 30 points
* Updating routes: 20 points
* Testing: 4 points
