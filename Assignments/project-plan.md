---
layout: page
title: Preliminary Project Plan
permalink: /assignments/project-plan
parent: Assignments
nav_order: 4
---
# Project Plan **Due Wednesday October 9, 12:00pm (noon) ET**{: .label .label-red }
All projects will involve frontend and backend development of new features for our StackOverflow.
Once teams have been formed, you and your team will decide what kind of new feature you would like to build.
Your feature should be something that can be implemented within the timeframe allotted (5 weeks, plus 2 weeks of planning), and will be implemented in a fork of the main codebase.
In the coming weeks, we will provide tutorials and instructions for you to run the entire application in a local development environment, and also to deploy it to the cloud.
Given that you will be up-to-speed on the StackOverflow codebase (and have been introduced to TypeScript, React, NodeJS, and testing frameworks),
and that you will have a team of four, we expect that the feature that you propose will be somewhat more complex than the features implemented in the individual assignments.

Feel free to look at existing systems like [Stackoverlow](https://stackoverflow.com/), [Quora](https://www.quora.com/), [reddit](https://www.reddit.com/) and similar stack exchange sites for inspiration on new features to build. 
Examples of features that students might propose include:

* Allow users to pose and answer questions using Markdown
* Allow users to register and save a profile using some SSO tool for authentication
* Improve the accessibility of the UI for some class of user (e.g.: screen-reader user, low-vision user, user with color-blindness)
* Modify the code so that it is easy to switch to other persistence options: (e.g. Firebase, Supabase, Postgres + GraphQL)
* Modify the code to generate secure and documented APIs using [tsoa](https://tsoa.com/) and [swagger](https://swagger.io/).
*  Retarget the client to use the Chakra UI library
* Improve the quality of the tests
* Add direct messaging and other chat features
* Propose some cool app using the infrastructure in the starter code (REST, WebSockets, persistent database)

Please note that multiple teams might choose to propose the same feature, or a variation of that same feature - this is OK.

When considering your project, please keep in mind that you will be allowed to publicly post your project online: while your immediate audience for the project is the course staff, if you are ultimately looking for software engineering jobs or co-ops, this project can be a useful piece of your portfolio.


The project plan will include:
* Introductory problem statement
* User stories and acceptance criteria: high level description of how users will interact with your new feature. 
* Work breakdown: Define engineering tasks that will be necessary to implement your new feature. Map each task to a sprint. 

You should plan on spending the next two weeks (from Sep 25 until Oct 9) in a "Sprint -1" in which you will undertake organizational and research tasks to help you decide on a project and formulate your plan.

You should be in contact with your assigned TA mentor before you submit the project plan, so they can answer questions and make sure you are on the right track.  You may wish to share a draft of your plan with them *before* October 9 to get early feedback.

Your team will self-organize, as agile teams do, and will enhance and adapt its plan during the project lifecycle.
As such, the primary goal of this document is to *begin* the planning process, and *not* to produce a detailed plan that must be followed precisely.
The course staff will provide regular feedback on your project to help ensure that the scope of your project is appropriate.

We list page *maximums* for each section as general guidance of what we are willing to grade. Please do not feel compelled to use all of the pages provided, and remember that a diagram or table can be as expressive (or more) as a comparable amount of text.


## Problem Statement, User Stories and Acceptance Criteria (max 4 pages)
Your project plan should begin with a 1-3 paragraph introductory problem statement: what problem in StackOverflow does your (proposed) feature solve? Provide a paragraph (or two) that describes why you are interested in building this feature. 

Given the problem statement, develop 3 user stories that show how a user would interact with the feature. User stories are requirements specified in the following format 
"As a < type of user >, I want < some goal > so that < some reason >."
My conditions of satisfaction are < list of common cases and special cases that must work >.

Your user stories should cover the key behavior or qualities that your feature will provide.

Each user story should include conditions of satisfaction.
Please make sure that your conditions of satisfaction cover all the common cases and can be turned into testable behaviors.

Each user story and condition of satisfaction must have a priority (Essential, Desirable, or Optional).  The set of Essential items will constitute the "Minimum Viable Product". 

Some of the suggested projects above are primarily about some non-functional quality of the code base and have little or no user impact.  For these, you may want to write stories of the form "As a project owner, I want ...".  You still need to offer a reason why a project owner might want the proposed goal to be accomplished.

Do not provide more than three user stories. Your problem statement and description of user stories and conditions of satisfaction should be between 2-4 pages.

## Work Breakdown (max 10 pages)
Given the project concept that you have chosen and the functionality that you expect to implement to satisfy your user stories, define a breakdown of the work that will be necessary to complete the project.

A work breakdown includes all of the tasks necessary to accomplish the project, and will be an artifact that we will refer back to throughout the project to evaluate whether you are making satisfactory progress.
Consider all of the kinds of tasks that your team will need to perform, including knowledge acquisition, design, implementation, testing and documentation tasks.
It is hard to say (generically) how many work items are necessary.

Each task on the work breakdown should be assigned to exactly one team member (as primary responsible party), who should provide a "T-Shirt" estimate for how long it will take (along with a justification for that estimate).
Consider the dependencies between tests: perhaps an API needs to be designed and specified before implementation can begin; perhaps your development environment needs to be configured before anything else can proceed.
Assign tasks to sprints considering these dependencies.

Given the preliminary nature of your plan, we do not expect that you will know all of the details about precisely how to implement your feature such that you could break it down into tasks that you feel could be implemented in a day or two. Large tasks (those which you can not provide a responsible estimate for) must be accompanied by smaller “research” tasks that can be performed early on in the project. You may wish to provide deadlines by which the task must either be refined into smaller tasks (based on new knowledge gathered), or reworked/abandoned.

For example: Consider if you were proposing the "job advertisement" feature, without the experience of having completed it. It might be difficult to consider how to break down a task like "Implement the frontend components for ad video playback" into something that you could commit to doing within a day or two. Given that this is a task that can be delayed until the end of the project (no other tasks depend on it), it would be wise to consider having some tasks early on in the project, such as: "Find react components that embed video ads," and "Implement simple video player that does not synchronize playback." Completing these smaller tasks early would let you both demonstrate that some forward progress is being made, and also allow you to create a much more responsible estimate for how that last, otherwise insurmountably large task would take.

**Do not wait for your TA feedback to begin this work.** You probably know more about the details of your project then they do. It will be helpful for all concerned if your Project Plan lists the major unknowns or things that you expect to need help with-- this will help the TA provide more useful feedback for you

Be realistic, and leave time for contingencies (including the time around the midterm exam in week 9).
Remember that you will need to have a demo prepared of your feature by project deadline - just 7 weeks from the due date of this assignment.
If you are uncertain that some tasks will be feasible, then be sure to include evaluation tasks earlier-on in the project that will allow for "go/no-go" decisions to move forward on a task or drop it.

We understand that it is quite difficult to estimate the technical complexity of a new project (as you are doing in the case of this course).
We will provide you with feedback on this preliminary project plan, which you will use to produce a revised project plan (due 2 weeks later).
Throughout the project period, teams will meet regularly with their dedicated TA Mentor, who will help track progress on a week-to-week basis and help to determine when adjustments to the project scope are needed.

Each work item should contain the following information:
* Task to be performed
* User story (or stories) that this task relates to
* Team member responsible for completing the task
* T-shirt size estimate of how long will be needed to complete the task, using the following buckets:
    * Small: Can likely be completed by one team member in one sitting of less than 3-4 hours
    * Medium: Likely to require involvement of multiple team members, over the course of 1-2 days
    * Large: Currently unable to provide a responsible estimate. 
* A brief (1-2 sentence max) justification of how you reached the size estimate of the task 
* Milestone for delivering the task, chosen from one of the following:
  * Sprint 0: Oct 9-Oct 22
  * Sprint 1: Oct 23-Oct 29 (Sprint 1 is just a single week)
  * Sprint 2: Oct 30-Nov 12
  * Sprint 3: Nov 13-Nov 26

Your work breakdown should take the format of a simple textual list.
 
## Submission 
Your project plan should be submitted as a single PDF in Canvas to the assignment "Preliminary Project Plan."
Each team submits a single document to Canvas.

## Grading
The project plan will account for 10% of your project grade, and will be graded out of 100 points. The grading of the project plan is further broken down as follows:

### Introductory problem statement (5 points): 
* Receive full marks if there is a narrative consisting of 1-3 paragraphs that describes a specific problem that your project aims to solve.
* Receive partial credit if the narrative is present, but does not describe a problem that the project aims to solve

### User stories (15 points):
Your user stories taken together will account for 15% of your grade on this assignment.  Each user story will be graded as follows:
* Receive full marks if:
  * The user story fits the problem statement
  * The user story satisfies the INVEST criteria for good user stories (construed quite broadly)
  * The user story contains a priority (essential, desirable, extension).  
  * The user story includes conditions of satisfaction that cover the "normal" expected behavior of the feature, and any important error cases
  * Each condition of satisfaction is marked with a priority (essential, desirable, extension). 

The user stories must be numbered (1,2,3) and each the conditions of satisfaction must likewise be numbered (1.1, 1.2, 1.3) and laid out in a table for easy reference.

Remember that you will get full credit for delivering a minimum viable product (MVP) only if you deliver working implementations of all of your essential user stories and conditions of satisfaction.
  

### Work breakdown (80 points):
Your work breakdown will be evaluated holistically on the following rubric:

#### Coverage of tasks needed (20 points):
Receive full marks if the work breakdown includes all (reasonably expected) tasks to implement your feature, considering these kinds of tasks: 
  * Background research 
  * Design of interfaces and data types
  * Deployment of third-party services
  * Implementation
  * Testing
  * Documentation

It is not possible to state generically for all projects whether *all* of the above types of tasks are necessary.
However, we believe that this list is exhaustive (we do not expect other kinds of tasks).

#### Assignment of tasks (10 points):
Receive full marks if:
* Each element on the work breakdown is assigned to one team member
* The distribution of tasks of each size are roughly similar between the whole team (no single person is assigned significantly more or fewer tasks of one size)

#### Sizing of tasks (40 points):
Receive full marks if each element on the work breakdown:
* Has a size estimate (small, medium, or large) that is provided by the team member assigned the task.
* Has a responsible justification for that estimation
* Every "large" task:
  * Is accompanied by a reasonable explanation of why the team is unable to provide a responsible estimate
  * Is accompanied by at least one small or medium task, scheduled well-before the "large" task is due to be completed. We would expect that most of these research tasks are scheduled to sprint 0, or perhaps sprint 1.

#### Scheduling of tasks (10 points):
Receive full marks if each element on the work breakdown:
* Is assigned to a sprint
* There are no obvious constraint violations (tasks that logically must happen before others should be scheduled before them)
* There are no "Large" tasks scheduled in sprint 0
