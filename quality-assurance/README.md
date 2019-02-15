# The Agile Monkeys' Quality Assurance Guide 📖

<!-- Table Of Content -->
- [1. Introduction](#1-introduction)
- [2. Motivation](#2-motivation)
- [3. Testing](#3-testing)
    - [3.1 UI Automation Testing](#31-ui-automation-testing)
    - [3.2 Integration Testing](#32-integration-testing)
    - [3.3 End to End Testing](#33-end-to-end-testing)
    - [3.4 Automated Load Testing](#34-automated-load-testing)
    - [3.5 Manual Testing](#35-manual-testing)
- [4. Data Provisioning](#4-data-provisioning)
- [5. Environments](#5-environments)
- [6. Testing environment health](#6-testing-environment-health)
- [7. Entire application tests run at night](#7-entire-application-tests-run-at-night)
- [8. Test Completion Reports](#8-test-completion-reports)
- [9. Root Cause Analysis (RCA)](#9-root-cause-analysis-rca)
- [10. Synchronization between Developers and QA engineers](#10-synchronization-between-developers-and-qa-engineers)
- [11. Onboarding new QA Engineers](#11-onboarding-new-qa-engineers)
- [Appendix](#appendix)
    - [Links of interest](#links-of-interest)
<!-- Table Of Content -->

# 1. Introduction
In this document we are going to talk about **QA methodologies and processes** that can enhance Quality Assurance. Nowadays, in many companies, QA processes are done by hand, and that easily becomes a bottleneck for development teams.

We strongly believe that **automation** could **improve the delivery speed and quality** of the code by **shifting testing to the left** in the Software Development Lifecycle. Furthermore, it **reduces** possible **human errors** and provides standardized results that can be audited and compared against previous results.

> <p style="text-align: center;">“the cost to fix an error found after product release was four to five times as much as one uncovered during design, and up to 100 times more than one identified in the maintenance phase.”</p> <p style="text-align: center;"><b>The Celerity Blog</b></p>

Moreover, some of the following sections will explain the benefits of having healthy environments and being able to provision testing data efficiently.

In addition to the above, there are also some sections aiming to make sure that the Quality of applications are always meeting or exceeding the expectations.

# 2. Motivation
- Find bugs at earlier stages
- Speed up delivery by reducing QA engineers' workloads
- Increase consistency when testing
- Avoid human errors

# 3. Testing

# 3.1 UI Automation Testing
UI Automation tests verify that user flows in the application is as expected and that new components added to our applications do not introduce regressions or otherwise break previous flows.

## What we do
To start integrating UI Automation as part of the process of feature delivery. One of the benefits is that UI Automation code can be developed in parallel with feature work as acceptance tests while developers are creating the new application functionality.

The use of libraries such as Barista for Android Espresso tests and the Robot pattern help reducing boilerplate code and encouraging reusability of components. Moreover, React web applications can benefit from frameworks like React Testing Library, which is able to render and test React components of the application while ensuring good testing practices.

# 3.2 Integration Testing
Integration testing will ensure that a modification in code continues working as expected when interacting with other components.

## What we do
Build integration tests against each of the services we work with in order to ensure that the app continues to work as expected as the codebase grows and new features are implemented.

Integration testing can be done in two different layers:
- Integration tests mocking other services
- Integration tests hitting other real endpoints

The first one can be achieved by using integration testing module such as Dropwizard. Additionally, other services that the service under testing interacts with, are mocked.

On the other hand, we can also set up integration tests to hit real endpoints using tools such as RSpec. To run integration tests with RSpec it's necessary to build a testing application, for example in Ruby, able to connect to databases, queues, etc and has an http client to perform requests. The responses from the services would then be asserted against. It’s also possible to add tests that make assertions against headers and SSL/TLS certificates.

All integration tests for different services would be located in the same GIT repository. In addition, all QA engineers would create PRs, get their tests reviewed, and then merge those tests into the repository. Furthermore, tests can be run against all services at once or a subset of tests can be run against one or more specific services.

# 3.3 End to End Testing
End to End testing is performed to ensure that the full application works as expected from client to services. Having this type of testing provides a more accurate view of the App integrity.

## What we do

Create a solution that produces automated interactions with the application and verify that the output is what it is expected. This is achieved by running Automated UI Tests hitting real endpoints.

# 3.4 Automated Load Testing
Changes to the codebase may not have a noticeable impact on infrastructure when tested with a few requests per minute. However, they could have huge impact when the number of requests increases dramatically. Load testing helps to identify potential issues that aren’t visible with other types of testing but will occur under production load.

## What we do
By adding pipeline automation for load testing and using a framework like [Gatling](https://gatling.io/) or [Serverless Artillery](https://github.com/Nordstrom/serverless-artillery) to write session simulations we can ensure that any version of the code we want to test will not have negative impact on the application or infrastructure. Furthermore, results of these tests could be compared against previous results to look at resource usage, efficiency, and changes to metrics over time. 

This is another step in the process that provides developers and QAs with more confidence at the time that code is deployed.

These tests are run in Development environments on a regular schedule or after deploying a change to the system that changes traffic patterns or persistence in a concerning way. If problems are discovered, changes are rolled back until they are addressed.

# 3.5 Manual Testing
Following scripts to manually verify the functionality of an application is a repetitive, exhausting and error prone process. Despite all of these disadvantages, it is still used as part of the Software Development Life Cycle in order to verify certain vital paths of the application.

## What we do

To progressively reduce the amount of manual testing in favor of more automated testing.

We trully believe in automation and we think that adding to the team software engineers specialized in automated testing can provide the company with great advantages such as more bandwidth and resources focused on other areas of the business as well as faster feedback loops.

# 4. Data Provisioning
We should be able to provision an account with mock or real data in any state we require to perform a test. Furthermore, this provisioning of data would be specific and ephemeral for that test and should not affect any other test running at the same time.

## What we do

To build a framework able to easily provision accounts, orders, etc. This framework should have the ability to inject all the necessary data into queues, databases, etc in order to give developers and QA engineers the ability to test the desired functionality without the need to performing manual data creation steps in order to reach that state.

Furthermore, to have a “tear down” step after a test has been carried out that avoids permanently adding data to data stores that won’t be needed again.

For example:
```
Given an order is in transit
When the order is received
Then the status of the order is updated to “DELIVERED”
```

The *given* step will define the data that we have to provision. In this case, we will provision a new order and update all the necessary information in the system in order for it to be reflected as “IN TRANSIT”.

This means that *when* the next operation performed is to confirm a delivery, *then*, we can verify that the result of the query is as expected.

# 5. Environments
During the Software Development Life Cycle we will go through different environmental stages starting in `Development` and finishing in `Production`. These environments will vary from company to company.

If any environment is blocked, it can slow down the pace at which features are released.

## What we do
Combining some of the above solutions such as *integration testing* and *data provisioning* we believe that it is possible to have a `Development` environment in which many tests could be happening at the same time without affecting each other. As an enhancement to the above approach, and taking into consideration that it could be complex depending on the architecture, we should aim to create functionality and tooling to allow replication of a `Development` environment locally.

We also believe that while a `Development` environment does not necessarily need to be exactly the same as the `Production` environment, `UAT` should be an **exact replication** of a `Production` environment. This will ensure that the behavior observed on `UAT` will be the same as that observed in `Production` and no unexpected surprises or errors will crop up in production.

# 6. Testing environment health
It is **vital** to developers and QA engineers that the testing **environments are always healthy**.

## What we do
Running scheduled daily or hourly health checks on the testing environments and on individual services to verify that everything is up and running, as well as being able to identify what errors need to be addressed.

There could be a case in which a memory leakage or slowly manifesting regression is introduced which these tests could catch.

Results of these tests can be emailed (Daily health check) or sent to a Slack channel (hourly health check).

# 7. Entire application tests run at night
Daily test runs give you a complete view of how the application is performing and how it behaves under pressure.

## What we do
To run UI automation, integration, load, and performance tests of the entire application at night when the environmental load is low. 

The results are then combined and distributed as reports to the necessary teams.

# 8. Test Completion Reports
Developers and QA engineers should both be accountable for each feature that is released into production. A Test Completion Report (TCR) is a document that reflects that the feature to be released has been successfully tested with positive results.

## What we do
**Note:** Not necessary for Development environment

To issue a TCR written by a QA engineer for each feature that is released to UAT or Production environments, making sure that functionality has been thoroughly tested. This report should also contain load and performance checks when appropriate where results are compared against previous results.

The document should at least contain the following sections:
1. QA issuing TCR
2. Description of the change
3. Services/Infrastructure modified
4. New service version, artifact id and GIT SHA
5. Target environment
6. Tests performed and results
    - Unit tests
    - Integration tests
    - Load tests (Where applicable)
    - Performance tests (Where applicable)
7. Comparison of results versus previous versions
8. Conclusions/Sign off
    - QA Manager approval
    - Software Engineering Manager approval

# 9. Root Cause Analysis (RCA)
Be prepared to identify what has caused the issue and how we could avoid that issue from happening again.

## What we do
To have a process available where a “Root Cause Analysis” meeting is scheduled after an event that has had negative impact in the application occurred.

The “5 Whys” approach is carried in order to fully understand how the issue occurred and take actions to avoid the issue happening again.

The output is socialized to the rest of the team.

# 10. Synchronization between Developers and QA engineers
Having developers and QA engineers in sync means that defects and bugs are scoped at earlier stages. This can be achieved when there is a well defined task including acceptance criteria, contracts, and testing criteria.

## What we do
To have well defined stories that can be understood by anyone on the team in a way that allows any other member of the team to continue the work if necessary.

An example of a story below:
| | |
|-|-|
|__Description__|To create a new endpoint in <service-name> that retrieves information from <database-name> based on a given order number and returns a JSON object containing the order delivery address and date of order.<br><br>An error must be returned if the order is not found, there is a missing query parameter, or if there is a technical error.|
|__Acceptance Criteria__|- 200 OK, body returned contains correct order delivery address and date of order<br>- 404 is returned when order is not found or request is missing query parameter<br>- 500 error is returned when a technical error occurs|
|__Notes__|Endpoint contract:<br>HTTP Method: GET<br>Endpoint: https://<host>:<port>/<service-name>?orderId=<orderId><br>...<br><br>Expected response:<br>...<br>|
|||

By following the above story and contract, both developers and QA engineers start writing code and checking their results against each other's code. This improves cooperation and communication and allow the release of features at a faster pace.

# 11. Onboarding new QA Engineers
By having an onboarding document to which we can refer to, we could reduce the dedicated time required for knowledge transfer.

## What we do
To create an onboarding document in which new joiners are able to easily find information about:

- Requesting access to required infrastructure and applications
- Setting up their laptops for development
- Existing infrastructure
- Used testing tools
- Testing stages for each feature
- Best practices in the company
- Feature release process
- Creating bug stories
- Creating TCRs
- Pipelines
- FAQs

In addition to the above, a Buddy is assigned to new engineers joining the team to ease the sometimes overwhelming process of starting a new role.

# Appendix
## Links of interest
- [Espresso (Android)](https://developer.android.com/training/testing/espresso/)
- [Barista (Android)](https://github.com/SchibstedSpain/Barista)
- [Dropwizard testing](https://www.dropwizard.io/1.0.0/docs/manual/testing.html#integration-testing)
- [RSpec](http://rspec.info)
- [Selenium (Web)](https://www.seleniumhq.org/)
- [XCUITests (IOS)](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/09-ui_testing.html)
- [react-testing-library](https://github.com/kentcdodds/react-testing-library)
