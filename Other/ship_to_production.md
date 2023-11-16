# How Big Tech Ships Code to Production

Today, I want to give you an inside look at how your feature requests and bug reports make their way into the apps and websites you use every day.

## requirements Gathering

Shipping code all starts with the product team gathering user feedback and requirements. The product and engineering teams break this down into smaller work items or user stores.

## Sprint Planning

Developers then pick up items during sprint planning meetings. A sprint is typically 1-2 weeks long. For larger projects, work may carry over multiple sprints. Engineering managers or tech leads prioritize and sequence items across sprints to balance team capacity.

## Design & Code

Once the sprint is planned, developers start building. For larger initiatives, there is often an RFC or design document process to align on high-level architecture and technical approach upfront. Here is where some key processes come into play. Developers use Git or something similar for source control and create feature branches to build new functionality without impacting the main codebase. This isolates their work. When database schema changes are required, migration scripts are developed in branches as well. Schema migrations require thoughtful design and extensive testing due to the risk of data corruption.

## Review

Once the code is ready, they open a pull request for the team to review. This knowledge sharing catches issues early.

## Unit Test

After approval, it gets merged into the main branch after running comprehensive unit tests. These tests help catch bugs early.

## CI/CD pipeline

Once a feature lands in the main branch, it kickstarts the CI/CD pipeline. Tools like Github Actions and Jenkins automatically builds, tests, and deploys the code through multiple environments like dev, test and staging. Validating across environments is crucial. Staging should match production infrastructure for consistent validation. This reduces surprises down the line.

## QA Test

QA engineers thoroughly validate functionality, run regressions, security scans, performance tests, and much more. It's worth noting that some teams rely on developers to validate their own code instead of dedicated QA. It works for some products, but not all. When the build passes all checks, it goes to UAT.

## UAT

UAT stands for user acceptance testing. The product team, QA, and developers all validate the features together.

## Release

Release candidates that pass UAT proceed slowly to production. Some teams use techniques like canary release and feature flags to slowly roll out changes to reduce risk. For production rollout of schema changes, techniques like maintenance windows, read replicas, and rollback scripts reduce risk. Multi-phase migrations and feature flags help control access during the transition.

## Monitor

Throughout the process, SREs monitor metrics, logs, and traffic for any production issues. Bugs get prioritized and fixed. In addition, product and engineering teams also monitor analytics to make sure the feature works as expected and does not hurt key business metrics.

## Summary

In summary, your feature request takes a journey though design, development, testing, and incremental rollout before becoming part of the software you use everyday.
