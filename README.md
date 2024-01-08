# Application Development Design System

Developing applications is an art form. Every literary author and code developer has their own style. There is no right way to do it. Not only is there not a silver bullet correct methodology, but the landscape of popular opinion and tooling is changing rapidly and argumentatively. 

This document is a checklist of areas of Application Development that should be addressed during the lifetime of an application. 

Each development group should make an informed decision based on the options available and not rely on a single one-size-fits-all mentality. 

The best answer to any question about "What should we use?" should always be "It depends".

This document is a living document; Its information will grow and change.

*Please comment and communicate changes for this document!*

## Development Team Dynamics
A development team takes on many roles. No matter if it is a team of 50 developers or just one, the team must handle producing a functioning result. The most efficient teams are able to address all the aspects of Application development all by themselves. This allows the team to take responsibility for and resolve any situation that arises.

We often see Application Development roles separated into separate groups like a group that deals with infrastructure and another group that deals with webservice code. Though these groups can coordinate and produce an end result, it often results in a finger pointing game and slow turn around.

Each roll is not necessarily separate people, though the more hats a single person wears, the less focused they can be. Cross-training similar roles among team members can greatly improve productivity and responsiveness.

There are also role specific enterprise groups dedicated to improving communication between team role representatives so as to share, train, and improve all teams together. The enterprise groups do work targeted to help all development teams, but the actual team member that has a specific role will be the best point of contact for results about a specific project.

### Example roles in an Application Development team:
* Security
* Coding
* Infrastructure/Operations
* QA Testing
* Project Management
* Business Consultant

### Example team 1:
This is a single developer "team" and is too common of an occurrence. 

A single developer cares for several applications. There is usually a manager or project manager who helps determine priorities and communicates with customers. This developer does all the coding and unit testing. The developer also manages the build pipeline, hopefully not a manual build on the person's local machine, and deployments. Concerns with deployment environments, transparency, and security are pushed to other operations groups who have limited knowledge of the product.

Pros:
* Cheap
* Not complex to understand
* Job security

Cons:
* Siloed development often results in aged skill set
* Stressful for the developer
* Technical debt piles caused by lack of attention on a single application


### Example team 2:
Many people form a team to cover all the roles.

The team plans and coordinates changes with the customer. The team decides on tooling matching the product needs. The team builds, tests, and deploys changes. No one person is on the hook for all the things. With cross-training, the team can handle any event at any time.

Pros:
* Fast responsiveness to any situation
* Improved culture of working in a team
* Can resolve technical debt

Cons:
* Expensive
* Outsiders to the team lose control

## CI/CD Automation
Deploying an update to an application should not involve manual intervention. Human beings are prone to errors, forgetting, steps, and unavailability. It can also be daunting to train someone on the manual steps of a pipeline. 

Even authorization should be automated as part of the process. This is accomplished by producing transparent logging, notifications, and gates throughout the automation.

One example of transparency is integration with the CMDB (Configuration Management Database) which tracks an organization's known deliverables. The CI/CD automation pipeline should update the CMDB with the latest deploy information.

CI/CD Automation is also known as Separation of Duties. By using pipelines, no one person is responsible for the steps in the process.

See more information on repository Merging and Branching strategies for triggering automation.

Automation can cover infrastructure provisioning, code analysis, artifact deployment, alerts, integrations, etc. Be careful to spend your time creating automation wisely. There is the occurrence of spending too much on automation.
XKCD: Is it worth the time?

### Examples of CI/CD Automation:
* Jenkins pipelines
* GitHub/GitLab workflows
* Cloud specific tooling

### Example pipeline #1
This is a Jenkins pipeline setup by the development team.

A developer completes code and commits it to the team's repository. The code is reviewed and approved for triggering the pipeline. The pipeline copies the code, builds the application, runs tests, analyzes the code base, checks gates, and sends notifications to interested parties. The built artifact is then published.

### Example pipeline #2
This is a manual pipeline.

A Developer builds the artifact on their machine. The developer submits the built artifact to whatever group does the deployments.

Cons:
* What if the developer leaves?
* What if a step is forgotten?
* What logging is there?

## Testing
There are many forms of testing. Your team should determine what styles of testing are beneficial for your product and how to accomplish that testing.

Testing everything at all levels is expensive and not necessarily beneficial. Find the best ROI for time spent testing.

There are many tools for testing. There is no perfect tool, but there may be a best choice for your product.

The only bad choice is to not test. The next worse choice is to not have reproducible testing.

### Example testing types:
* Unit Testing / Coverage
* Atomic testing
* Integration Testing
* QA Testing
* End to End Testing
* Manual Testing

## Databases
Different types of databases have different pros and cons. Relational databases strongly enforce data cleanliness but can be slow when compared to key/value stores. Caching is super fast but can be complicated for invalidation.

Choose a data storage type that fits your application's profile.

Once your data is stored in a location, many consumers will want that data. Giving direct access to a data source clamps down the ability for that datasource to change. Any schema update will cause rippling side effects across all systems dependent on that data source. Instead of direct data access, it is strongly encouraged to put a service layer as a middle man to gain access to the data instead of direct access and allow changes to schema that the middle service layer can accommodate.

See Enterprise Services for information on data sharing

### Example Databases:
* Relational: Maria, PostGres, Oracle, SqlServer, etc
* Key/Value: Mongo, Firestore, etc
* Flat Files
* SQLLite
* In Memory
* Browser Local Storage/IndexDB

## Enterprise Services
The purpose of Enterprise Services is to have a central location to discover available data and provide policed access. This allows groups to synergize their data needs. This doesn't mean the data is public nor unprotected.

### Example Enterprise Services
* Apigee

## Caching
Caching can greatly increase the responsiveness of applications at the expense of complexity and possibly stale data.

Cached data should not be a source of truth, but only a view of the actual source of truth fitted for a specific need.

### Example caching methodologies
* In Memory
* Data Warehouse/Lake
* Cloud options

## Application Communication Architecture types
There are many ways to organize an application product so that its services communicate effectively and timely. Microservices have received a lot of attention but have their own drawbacks. Is all that complexity really worth it? A well organized monolith may have many pros over finely grained microservices.

There are many factors when choosing an architecture including the size of the product, developer knowledge, available tooling, expense, etc.

### Example Architectures
* Microservice
* Event drive
* Monolith


## Application Architecture layers
An application no matter its size has layers of functionality within it. Even minimal microservices have layers of concerns. Larger monoliths may have bundles of many concerns.

These concerns can be separated vertically in to domains, or horizontally in to Controllers, Business Services, and Data Access, or a combination of the two.

It is strongly suggested to untether your business logic from presentation. 

For instance, in the case of a Front End framework like React, Vue, or Angular, the presented user interface code should have little to no actual business logic mixed in with it. Move that code to services or other objects to allow them to be more easily tested and abstracted.

Another example would be a complicated deployment pipeline. Separate the steps in to generic substeps that can be reused in other pipelines and use environment variables to determine targets and credentials.

Making a planned decision will result in a much more maintainable application.

## Dependency updating cycle
Your application ages. And it ages poorly. Security concerns arise and code stagnates. Even the languages that are used become out of date. 

An application that has not been updated in a long time can be very hard to update to the latest versions. Sometimes impossible. Doing the updates more frequently lowers the overall impact of the updates and lowers long term costs.

Make sure your dependencies, environments, tooling, and any other versioned things are updated regularly.

Your team will need to decide how regularly based on the applications concerns like security risk, active development, costs, developer availability, etc.

A good rule of thumb is to update every application at least quarterly and if the application is under active development, update it every 2 week cycle.

### Common versioned dependencies
* dependencies/libraries
* environments
* languages
* servers
* development practices
* development environments
* CI/CD pipeline dependencies

## Choosing language/framework/tooling
Choosing what language/framework/tooling to use is often an overlooked decision point when starting an application.

Pick things that work well for your team. Supporting many language/framework/tooling on one team can be a maintenance nightmare and make it tricky to hire new teammates. Make sure everyone on the team is comfortable with the chosen language/framework/tooling. Sometimes training can open up options.

Be careful of following the technology cutting edge and leaving a trail of one-of products.

It also not a good idea to get stuck in choices that are deprecated or past their lifetime.

Some things that can help alleviate framework rot / overload:
* Cyclical updates that give quick response to framework updates and bring deprecations to the fore front
* Updating all the team's products to the same stack when a new stack is adopted so that the team stays in sync
* Using a decision process to pick new frameworks/languages/tooling
  * Is it well adopted by the industry (cool new shiny things may not last long)
  * Is it well documented 
  * Is it updated regularly
  * Do you really need it or is there something that already does this
  * *There is a great google document available that details the decision making process*

## Terraforming
There are two major targets for scripting: infrastructure environment and artifact deployment.

Terraform is great for infrastructure environment updates. Be careful deploying application artifacts through terraform. There has been great success using CI/CD pipelines like GitHub actions and Jenkins.

## Repository
There are lots of code repository options. The worst option is to not use one. The second worst option is to use a code repository incorrectly.

A good code repository allows you to be safe in deleting code (instead of commenting it out). It also enables branching strategies for keeping your production, development, testing, features, and other code states separate.

Make sure your team is agreement on your repository strategy and follows best practices.

Monorepos are a related repository decision. A monorepo allows an application to be subdivided in to parts but also remain in one repository. This allows sharing code between parts to be "easier". You have to decide if the added complexity is worth it. Monorepos also make it trickier to maintain clean boundaries between the sub parts of your application. Monorepos are powerful, but be wary. Use them correctly for the right reasons.

### Common repository options
* GitLab
* GitHub
* Bitbucket
* Subversion
* Cloud options

### Discouraged repository options
* flat files sharing
* shared drives
* CSV

## Merging/Pull Requests Branching strategies
Related to repositories is your branching strategy.

A common methodology is to have a branch that triggers your CI/CD pipeline. This branch is safeguarded so that merges to that branch require a second pair of eyes to approve the changes. Development work is then done in separate branches that are approved and merged to the deployment branch.

A good team building exercise is finding consensus on branch naming and strategy.

Teams of a single developer may not need as complex of a strategy even to the point of having only on branch to which changes are pushed and deployed. 

Make sure your branching strategy is a conscious team decision. It may be helpful to document the strategy in a file in your codebase.

## Eslint / code analytics
Your code sucks. If you don't think so, wait a few weeks and look at it again. Any seasoned developer knows that nothing sits still. There are always new things to learn and new ways of doing things. Languages add features, libraries are created and updated, and just our mental outlook changes. 

Tools like eslint, code analytics, and type checking can help discover problems as well as train developers on best practices. By using these types of tools, it is no longer developers fighting over their religious principles but everyone agreeing to conform to an unopinionated higher power.

There is eslint for most everything. Plug it in to your CI/CD as a gate and help train your team to write code everyone will enjoy.

Code Analytics are available in GitHub, GitLab, Sonar, and other sources. You will want to check with the ARB to make sure your code is being analyzed in a safe location based on your application's security level.

It is a powerful developer experience to have tooling checking your work for common mistakes as you code.

## AI Assisted Programming
AWESOME! Use it! But be careful that you aren't feeding sensitive code to a public facing AI that can then share that sensitive code with others. Rarely will this be a risk, but do be aware that whatever the AI sees it shares.

Do not blindly trust written AI code. It is often wrong.

AI can also help write unit test banks. Super powerful. Make sure your edge cases are covered as the AI may not be able to process all the context of your intent.

## Security
Burp scans are not comprehensive. Security should be considered at every level of application development. Overflow errors, authorization, authentication, injections, OWASP, all of the things.

For Browser applications, any javascript code is visible on the client. Be prepared for someone to hack the code. A

Any input or interaction needs to be validated for any application. Having an untrusting mindset must be developed and tuned.

Relatedly, Eslint and Code Analysis can greatly help improve code quality to alleviate some security concerns.

## Authentication & Authorization
Utah Id provides authorization. All your logins should use Utah Id accounts. Rarely (never) should you roll your own login. Very little language in this document is as definitive as this mandatory Utah Id usage; You're going to have long term issues, including security implications, if you play out of bounds. You've been warned.

Authorization is a completely different animal. Role management can be super complex involving groups, roles, hierarchies, etc. Or it can be as simple as marking someone as an "Admin".

Make sure your application correctly checks authorization in all layers, and domains. Automated Tests should be constructed to prove compliance. At the time of writing, there is no enterprise scanning of any sort to prove authorization security.

Authorization must be done on the server side away from user interaction and inputs. User interfaces should have authorization checks for user experience, but user interface checks should never be trusted as the user may have access to circumvent them.

## Documentation
> Good code is its own best documentation. ― Steve McConnell, Code Complete

Documentation is sought after, but if it isn't accurate, it is worse than not having it. Make sure to document things that make sense to document. Documentation should focus on why an application does something instead of what it does.

Other forms of documentation include an Archer package which should be completed at the outset of the project instead of at the end.

Tooling like Confluence, markdown files, and google docs can be helpful places to group documentation files.

## IDE
There is no best IDE. For a particular language/stack/framework you may have limited choices. We have seen it helpful for a team to use the same IDE to alleviate troubleshooting and configuration concerns.

Make sure your IDE is up to date. There may be features that you are missing that will greatly improve your productivity. A wise developer learns new tricks of their IDE over time. It is often helpful to watch other developers use the IDE to learn new ways of doing things. This type of learning is a great side effect of Paired Programming.

Your build process should not be based on a particular IDE nor IDE version. 

## Appendix
### State of Utah Design System
The Utah Design System gives guidelines for User Interfaces especially on the web.

### Tech Radar
Thoughtworks showcases a Tech Radar of trends in the industry. It makes sense that a development team has their own Tech Radar specific to their needs. Each developer has their own Tech Radar of things that interest them that doesn't have to match the team's Tech Radar, but the team should be in agreeance on what toolings to incorporate in to their applications. A single developer should never operate on their own to add new things to a product without consulting the team.

### POLA - Principle of Least Astonishment
Write code that doesn't astonish people. Code that is hard to read for others is a detriment no matter how cool it is. Sometimes developer astonishment is a training issue. Take the time to train the team on new techniques if this type of astonishment is common.

Astonishment on weird ways of doing things or bad coding should be refactored.

The best compliment a developer can give another developer is that a piece of code was simple to understand.

### Low Code / No Code
Low Code / No Code options are powerful. Common coding tasks can be replaced by a low code option that makes maintenance easier, and developer knowledge requirements lower.

Before starting a project, consider the development effort involved. If it makes sense to use a Low Code / No Code solution

### To type or not to type

### Books
There are many books and sites available on how to be a better developer. Every little bit of information helps. This document can't possibly cover every aspect nor be completely accurate.
