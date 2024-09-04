---
layout: home
title: CS4530, Fall 2024
nav_exclude: true
seo: software engineering
type: Course
name: CS4530, Fundamentals of Software Engineering
---

# {{ site.title }}: {{ site.tagline }}
{: .mb-2 }
{: .fs-6 .fw-300 }

{% if site.announcements %}
{{ site.announcements.last }}
 [Announcements]({{ site.baseurl }}{% link announcements.md %}){: .btn .btn-outline .fs-3 }
{% endif %}
## Overview
Building, delivering and maintaining successful software products requires more than being good at programming. Software engineering encompasses the tools and processes that we use to design, construct and maintain programs over time. Software engineering has been said to consider the "multi person development of multi version programs." Development processes that work well for a single developer do not scale to large or even medium-sized teams. Similarly, development processes that work well for quickly delivering a one-off program to a client cause chaos when applied to a codebase that needs to be maintained and updated over months and years. This class will begin to explore these tradeoffs throughout the entire software development lifecycle, with a particular focus on how these decisions affect the quality of the resulting software.

This class will serve as an introduction to the field of software engineering, covering key topics such as:

-   **Requirements gathering and specification** <br />How to make sure that you build the product that your customer really wants
-   **Designing code for reuse, for readability, and for scale** <br />How to avoid reinventing the wheel? What makes code readable? Where does performance fit into designs? When do we decide when to revisit old design decisions, and how do we replace them? Can we avoid the mistakes that past developers have made?
-   **How to organize your development process to collaborate effectively** <br />How do we communicate our designs with others? How do we structure and coordinate development activities? How do we measure the performance of these processes, and tweak them over time?
-   **How to ensure that your code works, is secure, and broadly speaking, "does the right thing"** <br />How do we measure different quality attributes like usability, scalability and performance? How do we minimize the cost of defects? How do we automatically test complex systems? Can we automatically prove the absence of some kinds of defects?

## Course Outcomes

- Students will be able to define and describe the phases of the software engineering lifecycle (requirements, design, implementation, testing, deployment, maintenance)
- Students will be able to explain the role of key processes and technologies in modern software development.
- Students will be able to productively apply instances of major tools used in elementary SE tasks.
- Students will design and implement a portfolio-worthy software engineering project in a small team environment that can be publicly showcased to recruiters.

### Course Delivery
The course will be delivered in a "traditional" lecture style. Prof Wand's section will be entirely virtual, and the other sections will be entirely on-the-ground, with no virtual participation option. You must attend the section for which you have registered, and you may not partner with students in other sections for the term project.

| Section       | Instructor                                                                | Meeting Time                                 | Meeting Place      |
|---------------|---------------------------------------------------------------------------|----------------------------------------------|--------------------|
| 1             | Prof Bhutta                                                               | MR 11:45 am - 1:25 pm                        | West Village G 106 |
| 2             | Prof Bhutta                                                               | TF 9:50 am - 11:30 am                        | EXP 204            |
| 5             | Prof Bhutta                                                               | T 11:45 am - 1:25 pm & R 2:50 pm - 4:30pm    | Dodge Hall 230     |
| 8             | Prof Bhutta                                                               | TF 3:25 pm - 5:05 pm                         | Shillman Hall 425  |
| 9             | Prof Wand                                                                 | W 6:00 pm - 9:20 pm                          | Online             |

## Course Project
The assignments and project for this class are designed to mirror the experiences of a software engineer joining a new development team:
you will be "onboarded" to our codebase, make several individual contributions, and then form a team to propose, develop and implement new features.
The codebase that we'll be developing on is a Fake Stack Overflow project. You will get an opportunity to work with the starter code which provides basic skeleton for the app and then additional features will be proposed and implemented by you!
All implementation will take place in the TypeScript programming language, using React for the user interface.

At the end of the semester, the instructors and TAs will evaluate all of the student projects, and select the best (in terms of usability, code quality, test suite quality, and overall design) to showcase on course website. 

The project will provide hands-on experience to complement the skills taught in this class, requiring students to be able to:
- Work effectively in a small team
- Enumerate and prioritize development tasks
- Propose, design, implement and test a new feature in an existing non-toy software application
- Write code that their team members can read and review
- Review teammates' code
- Analyze a proposed software architecture
- Use relevant software tools, such as:
  - TypeScript
  - Visual Studio Code (or similar IDE)
  - Git
  - Mocha and Jest
  - Postman

Select projects from Spring 2024 are hosted [in our project showcase](https://neu-se.github.io/CS4530-Spring-2024/assignments/project-showcase).

### Acknowledgements
This class and its contents were inspired by Software Engineering courses at various institutions, including:
* Columbia's Software Engineering Course, COMS W4156
* CMU's Software Engineering Course, [17-313](https://cmu-313.github.io/)
* GMU's Web App Development Course, [SWE 432](https://cs.gmu.edu/~tlatoza/teaching/swe432f19/home.html)
* NCSU's Software Engineering Course, [CSC 326](https://sites.google.com/a/ncsu.edu/csc326-software-engineering/) and its [iTrust term project](https://dl.acm.org/doi/10.1145/3183377.3183393), also Chris Parnin's [DevOps](https://www.engineeringonline.ncsu.edu/course/csc-519-devops-modern-software-engineering-practices/) course.
* Past iterations of CS4530 at Northeastern: [Spring 2024](https://neu-se.github.io/CS4530-Spring-2024/), [Fall 2023](https://neu-se.github.io/CS4530-Fall-2023/), [Spring 2023](https://neu-se.github.io/CS4530-Spring-2023/), [Fall 2022](https://neu-se.github.io/CS4530-Fall-2022/), [Spring 2022](https://neu-se.github.io/CS4530-Spring-2022/), [Spring 2021](https://neu-se.github.io/CS4530-CS5500-Spring-2021/)
* Past iterations of CS5500 at Northeastern, as prepared by Mike Weintraub, Mike Shah, Frank Tip and Joydeep Mitra ([Spring 2024](https://sites.google.com/view/sp24-cs5500/)).

This website is built using [Kevin Lin's Just the Class](https://kevinl.info/just-the-class/) Jekyll template. 
