# Application Development Design System

Developing an application is an art form. Every literary author and code developer has their own style. There is no right way to create art. Not only is there not a silver bullet correct tooling, but the popular opinion changes rapidly, oftentimes circling back on itself. 

This document contains a checklist of areas of Application Development that should be addressed during the lifetime of an application.

Each team should make deliberate decisions for their application on each topic in this document based on options available, instead of relying on one-size-fits-all nor its-how-we-have-always-done-it mentalities. Teams should develop a common tech stack to their applications to improve maintainability and support. This tech stack must change at a paced and strategic cadence so as to prevent application rot.

Our product is what our customers think of us. Aged and unmaintained applications with gross technical debt give a bad impression. To increase trust, always put the best foot forward aesthetically and through the use of thought-out technologies.

The answer to the question "What should we use?" is always "it depends". There are pros and cons to every decision. This doesn't mean ignore the decision, but to make an informed decision.

This document is a living document; Its information will grow and change. Please join the community adding input, improving content, and updating outdated content. Use the issue tracker, pull requests, and any other form of communication to help improve this document.

## Development Team Dynamics
A development team takes on many roles. No matter if it is a team of 50 developers, or just one, the team must handle producing a functioning result. The most efficient teams are able to address all the aspects of Application development all by themselves. This allows the team to take responsibility for and resolve any situation that arises.

We often see Application Development roles separated into separate groups, like a group that deals with infrastructure and another group that deals with webservice code and another group that deals with security. Though these disparate groups can coordinate and produce an end result, it often results in a finger pointing game and slow turn around. The better functioning team has all roles represented and on the hook for the same timelines and deliverables. All the pigs in one basket (see [chickens vs pigs in agile](https://www.visual-paradigm.com/scrum/scrum-pig-and-chicken/)).

Each role is not necessarily separate people, though the more hats a single person wears, the less focused they can be. Cross-training similar roles among team members can greatly improve team productivity and responsiveness.

There can also be role specific enterprise groups that are dedicated to improving communication between team role representatives. This allows sharing, training, and improving all teams together. The enterprise groups do work targeted to help all development teams, but the actual team member that has a specific role for the application will be the best point of contact for a specific project.

### Example roles in an Application Development team:
* Security
* Back-End Coding
* Front-End Coding
* Design / UX
* Infrastructure/Operations
* Automated Testing
* QA Testing
* Project Management
* Business Consultant

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## CI/CD Automation
Deploying an update to an application should not involve manual intervention. Human beings are prone to errors, forgetting steps, and unavailability. It can also be daunting to train someone on a process of manual steps. Though, in contrast, automation is fire and forget which often makes it easy to forget what exactly it is doing.

Automation also includes Separation of Duties and Authorization as part of the process. This is accomplished by producing transparent logging, notifications, and gates throughout the automation. By using automated CI/CD pipelines, the whole team is responsible for the successful resolution of all steps in the process.

Automation can cover infrastructure provisioning, code analysis, artifact deployment, alerts, integrations, etc. Be careful to spend your time creating automation wisely. There is the real possibility of spending too much on automation.

See [XKCD: Is it worth the time?](https://xkcd.com/1205/)

See the section on repository Merging and Branching strategies for triggering automation.

### Examples of CI/CD Automation:
* Jenkins pipelines
* GitHub/GitLab workflows
* Cloud specific tooling

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)
* UGRC [ugrc](mailto:ugrc@utah.gov)

## Testing
There are many forms of testing. Your team should determine what styles of testing are beneficial for your product and how to accomplish that testing. The end goal is to have repeatable tests that provide reliable metrics and run quickly.

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
* Scripted testing

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Databases
Different types of databases have different pros and cons. Relying on a single data source style may have severe bottle neck consequences to your application.

Choose a data storage type that fits your application's profile. Every application is different. Every module of an application is different. Find solutions that work well for your application.

Once your data is stored in a location, many consumers will want that data. Giving direct access to a database clamps down the ability for its schema to change. Any schema update will cause rippling side effects across all systems dependent on that data source. Instead of direct data access, it is strongly encouraged to put a service layer as a middle man to gain access to the data. Layered architecture allows changes to schema that the middle service layer can accommodate so that consumers require little to no changes, or changes can be versioned.

See Enterprise Services for information on data sharing

### Example Databases:
* Relational: Maria, PostGres, Oracle, SqlServer, etc
* Key/Value: Mongo, Firestore, etc
* Flat Files
* SQLLite
* In Memory
* Browser Local Storage/IndexDB

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Enterprise Services
The purpose of Enterprise Services is to have a central location to discover available data and provide policed access. This allows groups to synergize their data needs. This doesn't mean the data is public nor unprotected.

### Example Enterprise Services
* Apigee

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Caching
Caching can greatly increase the responsiveness of applications at the expense of complexity and possibly stale data.

Cached data should not be a source of truth, but only a view of the actual source of truth fitted for a specific need.

### Example caching methodologies
* In Memory
* Data Warehouse/Lake
* Cloud options

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)
* UGRC [ugrc](mailto:ugrc@utah.gov)

## Application Architecture types
There are many ways to organize an application so that its services communicate effectively and timely. Microservices have received a lot of attention, but have their own drawbacks including complexity and cost. Is the complexity of managing many little pieces worth the gain of simple pieces and decoupling? In contrast, a well organized monolith may have many pros over finely grained microservices. There are also the three concerns of communication: atomicity, async vs synchronous, and coordinated vs orchestrated.

There are many factors when choosing an architecture including the size of the product, developer knowledge, available tooling, expense, etc. Make sure to make an informed decision based on needs and not on buzz words.

### Example Architectures
* Microservice
* Event drive
* Monolith

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Application Architecture layers
An application, no matter its size, has layers of functionality within it. Even minimal microservices have layers of concerns. Larger monoliths may have modules of many concerns.

These concerns can be separated vertically in to domains, or horizontally in to Controllers, Business Services, and Data Access, or a myriad of combinations. Research in to the pros and cons of the different types can help you take a deliberate path in the design of your application.

It is strongly suggested to untether your business logic from presentation and data access, often termed MVC (Model/View/Controller). Breaking out logic pieces in to pure functions and other devices allows easier testing, targeted mocking, smaller change sets, and many more long term options.

Making a planned decision will result in a much more maintainable application. Design with your whole team in mind and not just your skill set. See Tech Radar for team skills road mapping tooling.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Dependency updating cycle
Your application ages. And it ages poorly. Security concerns arise and code stagnates. Even the languages that are used become out of date. 

An application that has not been updated in a long time (years, or months, even weeks...) can be very hard to update to the latest versions. Sometimes impossible. Doing dependency updates more frequently lowers the overall impact of the updates and lowers long term costs. We have even seen developers use this as a training tool to learn new features available to them in the updates.

Make sure your dependencies, environments, tooling, and any other versioned things are updated regularly.

Your team will need to decide how regularly, based on your application's concerns: security risk, active development, costs, developer availability, etc.

A good rule of thumb is to update and release every application at least quarterly; If the application is under active development, update it every 2 week cycle.

Do be wary of alpha versions, major releases, pre-releases, and other non-long-term-support versions. These can be troublesome as they are not yet ready for production usage and may require large refactors down the road. See Choosing language/framework/tooling for information on choosing technologies.

### Common versioned dependencies
* dependencies/libraries
* environments
* languages
* servers
* development practices
* development environments
* CI/CD pipeline dependencies

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Choosing language/framework/tooling
Choosing what language/framework/tooling/etc to use is often an overlooked decision point when starting an application. A comfortable tech stack is a powerful tool for productivity, but caution does need to be taken to prevent it from becoming stale. A stale stack can decrease productivity and create a high bar of entry for other developers to join the team.

Pick technologies that work well for your team. Supporting many languages/frameworks/tooling on one team can be a maintenance nightmare and make it tricky to hire new teammates. Make sure everyone on the team is comfortable with the chosen language/framework/tooling pertinent to their role(s). See Tech Radar for information about creating a team technology roadmap.

Also be careful of following the technology cutting edge buzz words. This often leaves a trail of one-of products that can be tricky to support. Careful research and foresight can allow the adoption of powerful new and upcoming technologies. Trying out new things for the fun of it can create havoc among team members.

It also not a good idea to get stuck in choices that are deprecated or past their lifetime either by poor choices or by staying too long with a tech stack. See Refactoring and Migrating for ways to move on in your life.

Some things that can help alleviate framework rot / overload:
* Cyclical updates that give quick response updates and bring deprecations to the fore-front
* Updating all the team's products to the same stack when a new stack is adopted so that the team stays in sync
* Using a decision process to pick new frameworks/languages/tooling
  * Is it well adopted by the industry (cool new shiny things may not last long)?
  * Is it well documented?
  * Is it updated regularly?
  * Do you really need it or is there something that already does this?
  * See [Ryan Thorstensen's Tech Adopt Guide](https://docs.google.com/document/d/1Kr7tcnuRraQyTomTBMr_kh6nYyfL1Qb1U0KC3n6UEhQ/edit?usp=sharing)

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Refactoring and Migrating
Code is bad. A wise man said the worst thing you can do is write code. Writing code locks in logic and no longer allows the customer to easily change their mind. But, alas, minds do change. So the code should change too. Good code makes it easier to change code by being written with loose coupling, automated testing, and clean code.

When refactoring, automated tests are a great tool to prove that the refactored code performs as expected. Even little changes can cause large side effects if you aren't careful.

See Eslint / code analytics for analysis tooling to help with refactoring.

Migrating an application to a new technology or a new system can be daunting. There are many approaches. Try to steer away from massive large effort migrations. Taking years to move a whole system can result in a painful transition as well as project bloat and vaporware.

There are many approaches. One possibility is the Strangle Technique where pieces of an application are migrated off separately. As each piece it is turned off in the old application and turned on in the new application until all the pieces are moved. This results in quick turn around and continual production. It does require some complexity as both systems have to be running and synchronized.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Infrastructure provisioning
Infrastructure is a resource. Cloud allows provisioning this infrastructure through scripting using terraform and other tooling. Using scripting makes the process repeatable (prod, test, dev all match) and documented. Be wary of making manual changes to infrastructure. Putting scripts in a versioned code repository has many benefits and few cons.

There are two major targets for infrastructure scripting: infrastructure environment and artifact deployment.

Infrastructure scripting is great for environment updates.

Be careful deploying application artifacts through terraform. There has been great success using CI/CD pipelines like GitHub actions and Jenkins for deploying applications that are generally more natural to the developers constructing hte artifacts. Tooling should be used that makes it easy for those using it to troubleshoot it. If tooling is used that a member of the product's DevSecOps team does not own, there will be gaps in supportability. Keep tooling, including access, rights, logs, ownership, etc, close to home for the development team so they can respond to any situation. Separating access, rights, logs, ownership, etc causes internal turmoil when things go wrong, inability to resolve issues, and productivity lapses.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Repository
There are many code repository options. The worst option is to not use one. The second worst option is to use a code repository incorrectly.

A good code repository enables branching strategies for keeping your production, development, testing, features, and other code states separate. A code repository should give easy access to CI/CD pipelining. Merge conflicts should be easy to resolve so that team members trust each other. It also allows you to be safe in deleting code from your code base (instead of commenting it out) to improve your code quality.

Make sure your team is in agreement on your repository strategy and follows best practices.

Monorepos are a related repository decision. A monorepo allows an application to be subdivided in to parts but also remain in one repository. This allows sharing code between parts of the code base to be "easier". But monorepos can be quite complex for pipelining and make it trickier to maintain clean boundaries between the sub parts of your application. Monorepos are powerful, but be wary. You have to decide if the added complexity is worth it. Use them correctly for the right reasons.

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
* email

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Merging/Pull Requests Branching strategies
Related to repositories is your branching strategy.

A common methodology is to have a branch that triggers your CI/CD pipeline. This branch is safeguarded so that merges to that branch require a second pair of eyes to approve the changes. Development work is then done in separate branches that are approved and merged to the branch that triggers CI/CD.

A good team building exercise is finding consensus on branch naming and strategy.

Teams of a single developer may not need as complex of a strategy, even to the point of having only one CI/CD triggering branch to which developer changes are pushed and deployed. 

Make sure your branching strategy is a conscious team decision. It may be helpful to document the strategy in a file in your codebase.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Eslint / code analytics
Your code sucks. If you don't think so, wait a few weeks and look at it again. Any seasoned developer has seen their favorite code turn to mush over time. There are always new things to learn and new ways of doing things. Languages add features, libraries are created and updated, and just our mental outlook changes. A long term developer is always looking for ways to be more expressive in their medium.

Tools like eslint, code analytics, and type checking can help discover problems as well as train developers on best practices. By using these types of tools, it is no longer developers fighting over their religious principles, but everyone agreeing to conform to an unopinionated higher power.

There is eslint for most everything. Plug it in to your CI/CD as a gate and help train your team to write code everyone will enjoy.

Code Analytics are available in GitHub, GitLab, Sonar, and other tooling. You will want to check with the ARB to make sure your code is being analyzed in a safe location based on your application's security level.

It is a powerful developer experience to have tooling checking your work for common mistakes as you code and helping you find gaps in your knowledge.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## AI Assisted Programming
AI IS AWESOME! Use it! But be careful that you aren't feeding sensitive code to a public facing AI that can then share that sensitive code with others. Do be aware that whatever the AI sees, it shares.

Do not blindly trust AI written code. It is often wrong. Developers know they also too are often wrong. So Ai pairing with developers can be a great support system.

AI can also help write unit test banks. Super powerful. Make sure your edge cases are covered as the AI may not be able to process all the context of your application's intent.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Security
Burp scans are not comprehensive and have incredibly large gaps in coverage. If you are relying solely on an outside source to vet your application's security, you will be hacked.

Security should be considered at every level of application development. Overflow errors, authorization, authentication, injections, OWASP, all of the things. Blindly trusting built in tooling like Spring Security can open holes in your application you did not expect. Every route, method, call, end point, and thing, should be looked at with a security mindset. 

Validation is a huge component of security. Bad data easily destroys an application. Validation in the user interface is super helpful for the user, but the only place validation is absolute necessity is in the back end application code. Do not store nor work with any data that has not been properly vetted and validated.

For Browser applications, any javascript code is visible on the client. Be prepared for someone to hack it.

Having an untrusting mindset must be developed and tuned.

Relatedly, Eslint and Code Analysis can greatly help improve code quality to alleviate some security vectors.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Authentication & Authorization
Utah Id provides authorization. All your logins should use Utah Id accounts. Rarely (never) should you roll your own login. Very little language in this document is as definitive as this mandatory Utah Id usage; You're going to have long term issues, including security implications, if you play out of bounds. You've been warned.

Authorization is a completely different animal than authentication. Role management can be super complex involving groups, roles, hierarchies, etc. Or it can be as simple as marking someone as an "Admin" or defaulting to "public".

Make sure your application correctly checks authorization in all layers and domains. Automated Tests should be constructed to prove compliance. At the time of writing, there is no enterprise scanning of any sort to check authorization security.

Authorization must be done on the server side away from user interaction and inputs. User interfaces should have authorization checks for user experience, but user interface checks should never be trusted as the user has access to circumvent them.

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Documentation
> Good code is its own best documentation. ― Steve McConnell, Code Complete

Documentation is sought after, but if it isn't accurate, it is worse than not having it. Make sure to document things that make sense to document. Documentation should focus on why an application does something instead of what it does.

Other forms of documentation include an Archer package which should be completed at the outset of the project instead of at the end.

Be wary of people asking solely for documentation, as their focus is often not so much on the end result of a development lifecycle. Making your published endpoints self-documenting, user interfaces intuitive, and having just a good user experience goes a long way from lessening the need for separate documentation needs.

If you do write documentation, make sure to have built in reoccurring tasks in your sprints to review and update the documentation because it will rot and die.

### Some Documentation options
* repository README.md and other markdown files
* JSDoc/JavaDocs and other similar in-code commenting (often can generate docs from the comments)
* Confluence
* Swagger and other API describing tooling

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## IDE
There is no best IDE. For a particular language/stack/framework you may have limited choices. We have seen it helpful for a team to use the same IDE to alleviate troubleshooting and configuration concerns.

Make sure your IDE is up to date. There may be features that you are missing that will greatly improve your productivity. A wise developer learns the new tricks of their IDE over time. It is often helpful to watch other developers use the IDE to learn new ways of doing things. This type of learning is a great side effect of Paired Programming.

Teams need not all use the same IDEs, though this may sometimes result in configuration concerns. On the flip side an application that requires everyone to use the same IDE may have poor configuration or architecture concerns that should be resolved. Your build process should not be based on a particular IDE nor IDE version.

IDEs also often have some sort of config file that they read that will enforce coding styles. IntelliJ has its .idea folder. VSCode has a .editorconfig file. Deciding on common styling and committing these files with your product source can help a development team produce code that is easier understood by team members. See Principle of Least Astonishment.

### Some popular IDEs
* IntelliJ
* Visual Studio
* Netbeans
* Eclipse
* XCode
* text editor (notepad++, bbedit)
* vim
* language/environment specific environments

### Knowledge Consultants Contacts
* DTT [dts_dtt@utah.gov](mailto:dts_dtt@utah.gov)

## Appendix
### State of Utah Design System
The Utah Design System gives guidelines for User Interfaces especially on the web. Use it.

See [Utah Design System](designsystem.utah.gov)

### Tech Radar
Thoughtworks showcases a Tech Radar of trends in the industry. It highlights technologies that are Hold, Assess, Trial, and Adopt. Teams that discuss and determine statuses of technologies they are using and would like to use can help them form a roadmap for continued productivity.

It makes sense that a development team has their own Tech Radar specific to their needs. Each developer also has their own Tech Radar of things that interest them individually that doesn't have to match the team's Tech Radar.

The team should be in agreeance on what toolings to incorporate in to their applications no matter personal opinions. A single developer should never operate on their own to add new things to a product without consulting the team.

### Last Responsible Moment
> The last responsible moment (LRM) is the strategy of delaying a decision until the moment when the cost of not making the decision is greater than the cost of making it. - Software Architect's Handbook by Joseph Ingeno

Delay major decisions until they have to be made. You don't have to decide to buy the big expensive relational database until actually need it, which is probably never. You don't have to make everything microservices until you are actually building things. By making major decisions later, you have more information and can make a better decision.

### Principle of Least Astonishment (POLA)
> In user interface design and software design, the principle of least astonishment (POLA), also known as principle of least surprise, proposes that a component of a system should behave in a way that most users will expect it to behave, and therefore not astonish or surprise users. The following is a corollary of the principle: "If a necessary feature has a high astonishment factor, it may be necessary to redesign the feature." - [Wikipedia](https://en.wikipedia.org/wiki/Principle_of_least_astonishment#:~:text=In%20user%20interface%20design%20and,not%20astonish%20or%20surprise%20users.)

Write systems that don't astonish people. Code, scripting, interfaces, documentation, etc that are hard to read for others is a detriment no matter how cool it is. 

Sometimes developer astonishment is a training issue. Take the time to train the team on new techniques if this type of astonishment is common.

The best compliment a developer can give another developer is that a piece of code was simple to understand.

See also Tech Radar

### Low Code / No Code
Low Code / No Code options are powerful. Common coding tasks can be replaced by a low code option that makes maintenance easier, and developer knowledge requirements lower.

Before starting a project, consider the development effort involved. If it makes sense to use a Low Code / No Code solution use it.

Be careful of easy entries that then turn in to complicated messes. It may be easy to setup the initial solution, but hard to add future features. Not all that glitters is gold.

### To type or not to type
There are typed and untyped coding languages. There are definite pros and cons as well as strong opinions about which are better. The best opinion is that "it depends". 

We have found that strongly typed languages can help a team of developers better understand each other's intent, lower the mental load of what keys are in what objects, help discover null/undefined errors, discover surprising errors, and make refactoring efforts easier. It does take more training to learn typing, code tends to be more verbose, and getting the type system to accept a simple line of code can become complexly painful.

Single developer or small teams may not need typing benefits. A large team may not survive without them.

Maybe a discussion about tabs vs spaces will be less infuriating...

### Books / Websites / Information
There are gobs and gobs of books, sites, and other information available on how to a design a better application. Every little bit of information helps. This document can't possibly cover every aspect of application design nor be completely accurate. Do your homework. 

#### Books
* Software Architecture, the hard parts
* Code Complete

### Who to trust
Be wary of outside influencers who do not have a vested interest in your product. They have may have good intentions, but also may have personal opinions that are expressed in the absolute. Always look for voices that give pros/cons instead of naming technologies. Having an outside source setup tooling for your team may sound good at first, but will become a maintenance pain point later. If your team does not own something, chances are that that something will fade and age and lose support.

> The road to hell is paved with good intentions - anonymous

### Architecture Decision Records
As your team discusses and decides on the team's technical direction, it is often helpful to make note of these decisions. Architecture Decision Records are a formatted way to record this information. This can help refresh memories as well as train new members of the team.

See [Architecture Decision Records](https://adr.github.io/)

# TODO
* [ ] move each section to its own file and make readme a table of contents? or have links to make a table of contents at the top and each section has a "back to top"? or have it generate this readme from separate files to make it easier to find stuff for updating and smaller pull request targets?
* [ ] make the "see" things actual links
