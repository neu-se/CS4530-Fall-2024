---
layout: assignment
title: "Individual Project 2"
permalink: /assignments/ip2
parent: Assignments
nav_order: 2
due_date: "---"
submission_notes: Submit via GitHub Classroom.
---

Welcome back to the Stack Overflow team! In this second deliverable, you will be implementing new and exciting features to enhance the frontend interface and bring the web application to life. This assignment builds on the foundation you laid in the first project and will deepen your skills in frontend development with TypeScript and React.

## Objectives of this assignment
The objectives of this assignment are to:
* Investigate and understand a large, existing codebase
* Write new TypeScript code that uses asynchronous operations
* Write test cases that utilize mocks and spies
* Write React components and hooks that make use of state

## Getting started with this assignment
Start by accepting our [invitation](https://classroom.github.com/a/NtWcqIYx). It will create a Github repository for you which will include the starter code for this assignment. Run `npm install` within `./client` and `./server` to fetch the dependencies.  

{: .note }
**System-level dependencies:** The libraries used for React require some native binaries to be installed -- code written and compiled for your computer (not JavaScript). If you run into issues with `npm install` not succeeding, please try to delete the `node_modules` directory and re-run `npm install`. If the issue still persists, please leave a post on Piazza or come to Office Hours for assistance.

**Configuring Jest and VSCode**: If you would like to use the built-in Jest test runner for VSCode (where it shows the tests and their status in the sidebar), the easiest way to accomplish this for this project is to open *just* the `client` directory or just the `server` directory in VSCode - not the top-level directory. If you have a quick-fix to make it work with the whole project at once, please feel free to share on Piazza, and we will incorporate that here. Otherwise, you can use the Jest Runner extension to run each test individually.

**Running the app**: We strongly encourage you to interactively experiment as you develop by running the entire application in your development environment. 

## Grading
This submission will be scored out of 200 points, 180 of which will be awarded based on the correctness of your implementation, with the remaining 20 awarded based on your code style.

Your code will be manually evaluated for conformance to our [course style guide](https://neu-se.github.io/CS4530-Fall-2024/policies/style/). This manual evaluation will account for 10% of your total grade on this assignment. We will manually evaluate your code for style on the following rubric:

To receive all 20 points:

- All new names (e.g. for local variables, methods, and properties) follow the naming conventions defined in our style guide
- There are no unused local variables
- All public properties and methods (other than getters, setters, and constructors) are documented with JSDoc-style comments that describe what the property/method does, as defined in our style guide
- The code and tests that you write generally follows the design principles discussed in week one. In particular, your design does not have duplicated code that could have been refactored into a shared method.
- No duplicate code is allowed. 

We will review your code and note each violation of this rubric. We will deduct 4 points for each violation, up to a maximum of deducting all 20 style points.

Your code will automatically be evaluated for linter errors and warnings. 

- Each lint error or warning will result in a deduction of -3 points (up to a maximum of 30 points).
- This will not affect the 20 style points.
- Line endings will not be counted as errors.

The starter code comes with some lint problems, You are expected you to fix these linter problems, many of them will be fixed as you implement the tasks. 

You can run the following command within the client or server to fix some common lint errors
```
npm run lint:fix
```

## Implementation Tasks
This deliverable has three parts; each part will be graded on its own rubric. You should complete the assignment one part at a time, in the order presented here.

**General Requirements**: Implement your code *only* in the files specified.

You should not install any additional dependencies. **'package.json' must be unchanged**.

{: .note }
Refer to [IP1](https://neu-se.github.io/CS4530-Fall-2024/assignments/ip1) for instructions related to setting up MongoDB and running the client and server.

{: .note }
**GitHub Copilot:** If you haven't yet used GitHub Copilot, this might be a good time to set it up. It can be very helpful for writing boilerplate code, and especially for proposing implementations of very simple methods. You likely will find it very useful for many of these implementation tasks. To get it for free: 1. Sign up for [GitHub's Student Pack](https://education.github.com/pack) and wait for your student status to be verified, then 2. Install the [GitHub Copilot extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) for VSCode.

### **Task 0: Setup Environment Variables**

1. Create a file called `.env` in `./client`. In `./client/.env` ensure the following lines:
```
REACT_APP_SERVER_URL=http://localhost:8000
```
2. Create a file called `.env` in `./server`. In `./server/.env` ensure the following lines: 
```
MONGODB_URI=mongodb://127.0.0.1:27017
CLIENT_URL=http://localhost:3000
PORT=8000
```

### **Task 1: Implement refactoring of main components using custom hooks (32 points)**

We are going to refactor a few components to extract its state and business logic into a reusable custom hook, improving separation of concerns and keeping the presentation layer clean.

#### Steps to Achieve This

##### In Client

1. **Create hooks folder under src**  
   In `./client/src`, create a folder with name hooks. You will be storing all the custom hooks files in this folder.

2. **Create useAnswerForm custom hook for NewAnswer component**  
   Create a new file `./client/src/hooks/useAnswerForm.ts`. In this file, you would be implementing the useAnswerForm custom hook, which manages the state and logic for submitting an answer.
   The postAnswer function should validate the input fields and submit the answer using the addAnswer service.

3. **Update and remove the state management from NewAnswer component**  
   In `./client/src/components/main/newAnswer/index.tsx`, update the component to use the useAnswerForm hook.
   Remove the state management and form submission logic from the component.
   Use the returned values from the useAnswerForm hook to manage the form’s input fields and error messages.
   Ensure that the form submission now uses the postAnswer function from the hook.

4. **Create useHeader custom hook for component Header**  
   Create a new file `./client/src/hooks/useHeader.ts`. In this file, you would be implementing the useHeader custom hook, which manages the state and logic for input changes and triggers a search action on 'Enter' key press. This hook will accept the same props as that of `Header` component. Check the next step to know what it should return and the logic to handle the input changes.

5. **Update and remove the state management from component Header**  
   In `./client/src/components/header/index.tsx`, update the component to use the `useHeader` hook.
   Remove the state and the input handling logic present and use the `useHeader` custom hook without breaking any existing functionality.

6. **Create useTagSelected custom hook for component Tag**  
   Create a new file `./client/src/hooks/useTagSelected.ts`. In this file, you would be implementing the `useTagSelected` custom hook, which will handle fetching tag details by tag name. This hook should take the same parameters as the props in `Tag` component. It should also be responsible for fetching the tag from the server in case the value of the name field changes in the supplied object of type `TagData`. For this take a look at index.tsx in `./client/src/components/tagPage/tag/index.tsx`

7. **Update and remove the state management from component Tag**  
   In `./client/src/components/tagPage/tag/index.tsx`, update the component to use the `useTagSelected` hook. Remove any state management logic present along with any logic that interacts with an external system. Now use the `useTagSelected` custom hook in a way that the component works the same way as before.

8. **Create useVoteStatus custom hook for component VoteComponent**  
   Create a new file `./client/src/hooks/useVoteStatus.ts`. In this file, you would be implementing the `useVoteStatus` custom hook, to handle voting logic for a question. It will manage the current vote count user vote status (upvoted, downvoted), and handles real-time vote updates via socket events.

9. **Update and remove the state management from component VoteComponent**  
   In `./client/src/components/voteComponent/index.tsx`, update the component to use the `useVoteStatus` hook. Remove any state management logic present along with any logic that interacts with an external system. Now use the `useVoteStatus` custom hook and make sure the component works the same as before.
    
10. **Create useNewQuestion custom hook for component newQuestion**  
   Create a new file `./client/src/hooks/useNewQuestion.ts`. In this file, you would be implementing the `useNewQuestion` custom hook, which manages the state and logic for posting a question. The postQuestion function should validate the input fields and submit the question using the addQuestion service.

11. **Use the useNewQuestion custom hook**
   In `./client/src/components/main/newQuestion/index.tsx`, update the component to use the `useNewQuestion` hook.
   Remove the state management and form submission logic from the component.
   Use the returned values from the `useNewQuestion` hook to manage the form’s input fields and error messages.
   Ensure that the form submission now uses the postQuestion function from the hook.

12. **Create useMainPage custom hook for index.tsx in Main component**  
   Create a new file `./client/src/hooks/useMainPage.ts`. In this file, you would be implementing the `useMainPage` custom hook, which manages the page rendering logic for components such as `HomePageClass`, `TagPageClass`, `AnswerPageClass`, `NewQuestionPageClass`, and `NewAnswerPageClass`.

13. **Use the useMainPage custom hook**
   Refactor the Main component located at`./client/src/components/main/routing/Main.tsx` to use the `useMainPage` custom hook for managing page switching and states. This will simplify the logic in Main and allow centralized page management within the useMainPage hook.

14. **Create useLoginContext custom hook**  
   Create a new file `./client/src/hooks/useLoginContext.ts`. In this file, you would be implementing the `useLoginContext` custom hook, which will access the `LoginContext` using the `useContext` hook and return it.

15. **Update and remove the state management from component Login**  
   In `./client/src/components/login/index.tsx`, update the component to use the `useLoginContext` hook.
   Remove the line that uses the `useContextHook` to access the `LoginContext` and instead use the `useLoginContext` hook to access the `LoginContext` making sure that the Login component works the same as before.

16. **Create useUserContext custom hook for component Login**  
   Create a new file `./client/src/hooks/useUserContext.ts`. In this file, you would be implementing the `useUserContext` custom hook, which will access the `UserContext` using the `useContext` hook and return it.

17. **Use the useUserContext custom hook**
   Identify the components that are using the the UserContext. Use `useUserContext` custom hook in them to get the `UserContext` instead of directly accessing it using the `useContext` hook.

You do not need to write tests for this task, but after completing this task, your frontend should run without any issue.

Grading for implementation tasks:
* `useAnswerForm`: 4 points
* `useHeader`: 4 points
* `useLoginContext`: 4 points
* `useMainPage`: 4 points
* `useNewQuestion`: 4 points
* `useTagSelected`: 4 points
* `useVoteStatus`: 4 points
* `useUserContext`: 4 points


### **Task 2: Implement Comment feature (108 points)**
In our current software, a missing feature from StackOverflow is the ability to comment on questions and answers. We are going to add Comment feature in this task

#### Steps to Achieve This
##### In Server
1. **Create Schema and Model for Comment**  
Follow the documentation in `./server/models/schema/comment.ts` to add fields to the schema. Then, add the `comments` field in both `./server/models/schema/question.ts` and `./server/models/schema/answer.ts`. Next, in `./server/models/comments.ts`, create and export `CommentModel`.

2. **Define types for Comment**  
In `./server/types.ts`, follow the documentation to create the `Comment` interface and `CommentResponse` type. A `CommentResponse` can be either a `Comment` or an error message. Next, modify existing interfaces for `Question` and `Answer` to add a property for `comments`. **You may also need to modify existing instances of `Question` and `Answer` after the change.**

3. **Implement `saveComment` and `addComment`**  
In `./server/models/application.ts`, follow the documentation to implement `saveComment` and `addComment`. For `addComment`, follow existing tests in `./server/tests/application.spec.ts` for how to handle errors. Add additional tests for `addComment`. **Make sure that the tests pass before moving on to the next step.**

4. **Modify `populateDocument` and `fetchAndIncrementQuestionViewsById`**  
In `./server/models/application.ts`, modify `populateDocument` and `fetchAndIncrementQuestionViewsById` to also populate `comments`. **Make sure that the tests pass before moving on to the next step.**

5. **Create `AddCommentRequest`**  
In `./server/types.ts` follow the documentation to create the `AddCommentRequest` interface.

6. **Create the controller for Comment**  
Follow the documentation to implement all the functions used in the endpoint in `./server/controller/comment.ts`. Then, write tests in `./server/tests/comment.spec.ts` to test the newly implemented endpoint. **Make sure that the tests pass before moving on to the next step.**

After completing the above steps, the backend functionality of Comment should be working. **In addition to automated tests, you should also manually test your route using Postman and MongoDBCompass to ensure that your query is correct.**

##### In Client
1. **Define types for Comment**  
In `./client/src/types.ts`, follow the documentation to create the `Comment` interface, then add the `comments` property for `Question` and `Answer`. **You may also need to modify existing instances of `Question` and `Answer` after the change.**

2. **Implement `addComment` in `commentService.ts`**  
In `./client/src/services/commentService.ts`, implement `addComment`. It should call the `COMMENT_API_URL/addComment` to add the comment to the backend database.

3. **Create component for `Comment`**  
In `./client/src/components/main/commentSection/index.tsx`, implement the `CommentSection` component following the documentation.

6. **Use `CommentSection` in `Answer` component**  
`./client/src/components/main/answerPage/answer/index.tsx` is the component for an answer. Modify `AnswerProps` and add `CommentSection` to the HTML return statement.

5. **Use `CommentSection` in the Answer Page**  
`./client/src/components/main/answerPage/index.tsx` is the page for a question with detailed information. Implement `handleNewComment` that will be used as the handler in `CommentSection`. Add error handling as you see fit. Then, update the HTML code to include `CommentSection` component and the updated `Answer` component.

Grading for implementation tasks:
Backend: 42 points
* Schema and Model: 4 points
* `types.ts`: 10 points
* `saveComment`: 2 point
* `addComment`: 8 points
* `populateDocument`: 2 point
* `fetchAndIncrementQuestionViewsById`: 2 point
* `isRequestValid`: 2 point
* `isCommentValid`: 2 point
* `addCommentRoute`: 10 points

Frontend: 40 points
* `CommentSection`: 28 points
* `answer`: 4 points
* `answerPage`: 8 points

Testing: 26 points
* `addComment`: 6 points
* `addComment` route: 20 points

You can begin to implement these steps in whatever order you see fit, but we would suggest completing them in the order shown in the specification.

### **Task 3: Implement Communications using Socket.IO (40 points)**
We are using Socket.IO for some specific communication between the client and the server. For instance, in `./client/src/components/main/questionPage/index.tsx`, it is used to listen for real-time updates on questions and answers, allowing the client to automatically update the UI without requiring a manual refresh. Explore the codebase to get familiar with this concept.

For this task, you need to implement the missing code in `./client/src/hooks/useVoteStatus.ts` and `./server/controller/question.ts` for the ability to update votes, and `./client/src/components/main/answerPage/index.tsx` and `./server/controller/comments.ts` for the ability to update comments. If one of these files is missing, you need to revisit previous tasks to make sure that you create files correctly. Otherwise, search for "TODO: Task 3" in the entire codebase to find all places you need to implement code for this task.

You do not need to write tests for this task, but after the implementation, you should be able to view votes and comments changing in real time if you open two webpages at once.

Grading for implementation tasks:
* `useVoteStatus`: 14 points
* `question.ts`: 4 points
* `answerPage`: 14 points
* `comment.ts`: 8 points

## Submission Instructions
Submit your assignment in GitHub classroom, **all commits must be visible on the main branch on GitHub classroom to receive credit**. 

Once your submission is pushed to your main branch, GitHub will automatically run the grading script on your submission. Check the Actions tab on GitHub classroom to see the output of the grading script. 

![image]({{site.baseurl}}{% link /Assignments/ip2/ActionsTab.png %})

Refer to the grading section for a detailed breakdown of how your assignment grade will be calculated.   