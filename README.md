# WorkHound coding test

Thanks for your interest in an Engineering role at WorkHound, and congrats on advancing to this point! We'd like to see a sample of your software development work, in a context that is as close to day-to-day work as possible within the bounds of time and logistics.

Provided here is a base ExpressJS app created with the `express-generator` npm package. Within a **three-hour timebox**, build to the below specification as best you can. Please commit and comment as you would for a normal product feature, but feel free to elaborate in comments on thought process or deliberate omissions based on the time limit.

It is NOT required for your sample to run without error or be syntactically perfect, the goal is understand what it would be like to share a working codebase with you and to understand how you approach problems. Functions, methods, and tests can be stubbed as generously as you need to in order for you to demonstrate your solution to the problem within the time limit.

## Background

After a Worker in our platform submits feedback via SMS, we create a "Comment" object in our MongoDB with the text of their message. As we create this record, we also POST the text to a third party vendor for some additional analysis. This vendor's API is asynchronous, so after they have completed processing, they will issue a webhook POST request to us with their analysis.

## Assignment

Build the webhook endpoint for this vendor to POST their response so that we can consume it and add provided data to the `Comment` object.

## Context
- Based on the nature of this vendor, we must respond to their request with an appropriate HTTP response code as quickly as possible.

- Occasionally, this vendor may replay webhooks, a `Comment` object may have been manually modified or deleted by other parts of our system, or the webhook may be missing a payload altogether if the vendor is having certain types of system outages. We must NOT overwrite any manual data changes that may have happened before the webhook arrived, or between instances of a replay. Ideally we can indicate via response code when they should or should not retry.

- You may make any reasonable assumptions about the schema of our `Comment` objects, the payload from the vendor, or what the vendor may do in the case of various HTTP codes, but please document these along the way.

- We have a shared symmetric key with this vendor which they are supposed to send via `Authorization` HTTP header. We must confirm each inbound webhook includes this, and has been sent via HTTPS.

- We use [Bull](https://www.npmjs.com/package/bull) for queuing and delayed work in other parts of our codebase. You are welcome to use this library if your solution requires it, but this assignment has NO requirement to set up or communicate to a live Redis instance.

- We use the plain [MongoDB](https://www.npmjs.com/package/mongodb) driver for Node, so you can reference those docs for the interface available, though this assignment has NO requirement to set up or communicate to a live Mongo instance.

## Submission & Questions

Please fork this repository and open a Pull Request against it with your changes so we have a commit history. Your submission will be anonymized and evaluated by the engineering team, and if you're selected for a virtual onsite, one of your sessions will be reviewing your solution with some of our team.

No part of this assignment is intended to be a trick or a 'gotcha'. Any questions, concerns, process issues, or if you need clarification on any part, please send directly to jonathan@workhound.com
