# Stacked Commits

A couple of intro readings:

- <https://google.github.io/eng-practices/review/developer/small-cls.html>
- <https://benjamincongdon.me/blog/2022/07/17/In-Praise-of-Stacked-PRs/>

Stacked Commits is the idea that instead of doing PRs (peer reviews) at the level of (feature) branches we do them at the level of (feature) commits. This scale changes is important for two main reasons:

- It makes PRs a _lot_ easier because the smaller scale makes them easier to review and easier to understand. These combine to make PRs more efficient (and thus takes less time, effort, energy, and stress), because less time is spent sifting through the changes to get to the core biz logic changes, and more accurate, because the reviewer can be more thorough since the amount of changes is much less.
- The smaller scale also means more work can be concurrently woven together. The bigger the PR, the more likely there is going to be merge conflicts simply because its bound to have more changes that touch more parts of the codebases. But the smaller the PRs, the less likely there is going to be merge conflicts because the change would bound to touch less parts of the codebase. And if there is a merge conflict, dealing with it is less painful because, again, the conflict is happening in less places (because the change touched less parts of the codebase).

## Motivating Example

Lets say there are 3 developers and 3 stories.

Developers:

- Bucatini
- Tortellini
- Fettuccine

Stores:

- AB#01 add GET /ping endpoint that returns HTTP 200 and the message "I'm alive"
  - Release date: Dec 10
- AB#02 add Spanish language support to the GET /ping endpoint: "Estoy viva"
  - Release date: Dec 20
- AB#10 add international language support for all endpoints
  - Release date: March 1

### The conflicts that happen

In a mindset where you think at the scale of (feature) branches, it is tempting to combine AB#01 and AB#02 together into one Sprint because they depend on each other and leave AB#10 for another Sprint because its not directly related to the current initiatives and its deadline is later. The following are a few examples of conflicts that can happen when this is the case.

#### Developer vs Developer conflict

Bucatini and Tortellini hard at work trying to finish their stores in time to hit the release dates. Fettuccine tries to put the brakes on it, telling them that they need to slow down and not take any shortcuts: they need to take the time to do a "good", scalable implementation of Spanish support because later on the team will have to do full international language support. Bucatini and Tortellini push back and say that doing a full scalable implementation will take too long: not only at they fighting with the deadline but also with the code freezes that will happen because of the upcoming holidays. A messy conflict ensues and everyone leaves feeling bitter.

### Developers vs Product Manager conflict

Bucatini, Tortellini, Fettuccine are united in pushing back against the business: before we can do AB#01 and AB#02 we need to do AB#10 first. If we don't do the work of refactoring the codebase and building in the infrastructure needed to support AB#10 sh*t is going to hit the fan. The Product Manager feels betrayed because this initiative was a long time coming and the team made promises to another team that it would happen on the specified dates. Bucatini, Tortellini, Fettuccine push back and point out that they have been putting off paying down tech debt on promises that they will get a chance in the future "once this initiative finishes". Two initiatives later and the business is still pushing to ship, ship, ship without giving them a break to clean up their codebase and set themselves (and indirectly the business) up for future (continued) success. A messy conflict ensues and everyone leaves feeling bitter.

### Team vs Business conflict

The Team is united in their stance that they've rolled over long enough: they need to address growing problems with the maintainability and scalability of the codebase. The Business gives them the go-around never conceding. A messy conflict ensues and everyone leaves feeling bitter.

## Pitfalls

- Of course, what is a big vs small commit is subjective. So it is important that team establishes a rule for when to consider a commit too big. A rule of thumb is a good average size is about 100 line of code across max 3 files while a commit that is too big is typically 1000 lines of code across 10 or more files. REMEMBER: a commit can never be too small; in fact the smaller the better!
- It is also important to establish what is a complete and independent commit. A good start to defining what that is should include a rule that every commit should include both the change and a corresponding test for the change.
