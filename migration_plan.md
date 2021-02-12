Some say it cannot be done...

Or it's too scary to even attempt.

But an application is a living and breathing soul, that can get old with time.

As time passes, new frameworks appear, older versions are put to rest and the tech environment is always shifting and becoming better, faster and more reliable.

That means that your application may slowly be branded as... legacy.

This means that it's time for an update, it's time for a migration.

I have been reading a lot of articles lately and people tend to mix the concept of migration with refactoring.

That is why I wanted to write this article so I can share with you my 8 step plan for a flawless migration process.

But before jumping into that...

What is the difference between migrating and refactoring code?

Code migration is the movement of programming code from one system to another. There are three distinct levels of code migration with increasing complexity, cost and risk.

The simple migration - involves updating dependencies or the language version. For example migrating from PHP 5.4 to 7.0 can be considered a simple migration. Trust me, it doesn't feel like a simple job at all when you start doing it...

The next step would be the migrating to a completely different language. This is considered a more complex task as it involves changing the whle syntax of the code base.

The most difficult migration would be changing to a completely new platform or operating system.

In our case, migrating the Chip API in order to make it compatible with a new database version would be considered a complex migration.

But this doesn't make it an impossible task. Not by any means.

Even the most complex task can be achieved when you have the proper plan in place. I always like to say that if you don't have a good plan, than you are planning to fail from the start.

Let's address the elefant in the room first. I don't consider myself an expert in migrating code, but I have completed a fare share in my developer career, so i can say that I learned a few tricks.

I always started every migration with a plan and improved it after each successfull migration that I completed.

Every challenge is a good learning platform and migrating code brings some interesting problems that need to be solved.

Before you set yourself to the challenge, here are a few issues that you need to consider:

- Data integrity - If your migration involves data, then you need to make sure that no data will be lost in the process. Your database will need to be taken down when you decide to "press the switch" and complete the migration, so plan it ahead and don't lose any user data.

- Data security - Changing from a known provider to another one can open the door for security exploits. You must make sure that the security of your data will be improved and not lowered by your migration. Keep you passwords and environment variables secure during the process.

- Clueless end users - Durint the migration process your end users should not see any difference in the service provided. A good target would be to keep the users of your application clueless to the process taking place in the background.

- Minimal down time - As part of your migration process, you will probability need to take your app down or put your API in a teapot state for a couple of hours till when the switch needs to happen. Try to push changes as frequent as possible to production and leave as little code as possible to be migrated when the actual switching over needs to happen. 

- Migration does not equal refactoring - Some developers make the mistake of refactoring code during the migration process, thinking that they will improve the overall system. You need to stop doing refactoring as this will bring a new layer of complexity in your migration process. Try to focus on migrating te code over, even with the risk of copying some of the old system's bugs, make a note of all the bugs you encounter so you can fix them later as part of the post-migration tasks.

This are just some of the more important issues that you will have to deal with, but I am sure there are many more scenarios that you will encounter.

When working with legacy code, you never know what may be lurking beneth the calm look of the surface code...

Now that we talked about the problems, let's discuss the solution. The most important aspect of a migration process, is the preparation or how I like to call it, "The Plan".

Let's imagine that you are called into your Project Owner's office, on a Monday morning, and given the task to migrate a legacy PHP 5.6 system to a newer PHP 7.4 platform in order to make it compatible with the newest Mongo DB 4.4 database version.

This is somehow simillar to what my squad was tasked over the last couple of months at Chip.

We had to move code from a legacy API to a newer version in order to keep it compatible with the newest Mongo database version that we ended up implementing. 

To complete the process we spent around 2 months and in the end we:
- Removed around 550k lines of code
- Sunset an entire public api
- Removed all the background tasks and processes from our legacy platform and moved them to the new one
- Removed 3 docker images from our repo
- Updated our configs to increase security
- And prepared our platform for the next set of exiting improvements that are planned in the near future (will keep you posted)

But none of these would have been possible without the 8 steps plan.

Let's break it down...

1. Prepare the ground

During the intial sprint (or sprints), try to get familliar as much as possible to the whole system architecture. If you need to migrate from platform A to platform B, then take your time and explore of them. Take a closer look at what makes platform B a better home for your code.

After this intial step, you should be able to answer the question "Why do we need to migrate to the new platform?" with at least 3 benefits.

During this phase do some code exploration, and if time alows you, put a software architecture diagram on a piece of paper to give you a better idea about the dependencies of your code.

If you are working in sprints, then it would be a good idea to align the first sprint with this exploration step.

2. Create a multidisciplinary team

Migrating a legacy code is not a job for a single developer. Even if you are the next Robert C. Martin of the PHP world and have more then 10 years of experience under your belt, you will probabily need to rely on a team to help you complete this task.

For a mobile application, your may require the help of an Android and an iOS developer and for a backend migration you may need the sharp mind of a platform enginner and at least two QA engineers.

Pick your team carefully as these are the people who will support you through the tough times for the next couple of weeks. Team chemistry is very important and sometimes it can make or break a migration process.

3. Have a logging system in place

If you don't already have a way of logging events coming out of your system, then you need to put aside time to implement one before starting this journey. At Chip we use DataDog which is one of the best solutions for monitoring cloud based applications. 

This will be critical in discovering critical parts of your application that needs to be migrated first, or dead code that can be removed. You can also use the logs to discover bugs introduced by your migration and fix them as part of the post-migration tasks.

At Chip we rely heavily on our logs to discover issues happening in the code, but also to take data driven decisions for the features that we want to plan ahead.

4. Code tests are your best allies

Before even considering a migration or refactoring job, you need to have a good test coverage. If you plan to keep the same functionalities of the application while performing the migration, then you will need to define those functionalities by writting tests.

I am not just talking about unit tests, but also functional tests and api tests. The more tests you write at the beginning of your project, the least you will have to worry about introducing unwanted behaviour in your application.

Consider writing higher level tests that will cover your api but not your low level implementation. If you are moving the code to a new platform, then you need to make sure that it behaves in the same way once the process is completed.

5. Decide on a version control branching flow

Are you going to deploy code as frequent as possbile or just have a long standign branch that can be deployed when the migration process is completed?

From my experience, the best approach would be a combination of the two. Of course your project may be different and this should be judged case by case, but most of the times you will encounter situations where some parts of the code can be deployed as soon as they are migrated, but some other parts are more coupled and need more attention.

For example in a migration to a newer database version, some models may not work with the new version of database and may require switching the persistence layer first, then update them. In this case a long standing branch may be a better solution for the code that cannot be deployed immediately.

This is exactly what we decided to do as part of our task at Chip. We deployed the code that was compatible with the older Mongo DB version, but we kept the code that required the new version on hold, to be released after the database upgrade.

6. Break the process in tasks

One major issue that I encountered in my early career was dealing with tasks that wee too big to handle and were blocking others from making progress. 

Try to break your migration process in tasks that have a single clear objective. This will help you and the team members to work individually and in parallel on the same system.

For example, if you receive a task titled "Complete the migration" then that one probabily needs to be broken apart. if your task is too broad in it's scope then you will eventually end up blocking the progress of other team memebrs who are waiting for you to deploy your work.

At Chip we use Jira as a software development tool to track our tickets and organize our sprints. This gives us clarity and helps us manage teams of developers with ease. As a developer, it's always nice when you can clearly see what your tasks are for the entire sprint.

7. Create a QA plan

Before doing the big leap of faith, you need to properly test your code and make sure it works in the same way as it used to work in the old platform.

The developers can test their own code, of course, but we all know how we sometimes skip the parts that may be broken and put more accent on the parts that we know they "work already". You may be very happy that all your tests pass, but this is not enough for a big and complex application.

You need an outside person who hasn't worked on the initial code to try and break you code and discover if there are any hidden issues.

To do this, you will need a regression test. A regression test can be done by a skilled QA engineer and run multiple times before your application gets pushed into production.

At Chip we employ the help of an entire team of QA engineers to make sure our code is bug free before reaching the production environment. The team is split across mobile (front end) and backend QA engineers and we are always looking for the best talent out there to enhance our QA capabilities.

8. Press the red button

During our last migration at Chip, we had to bring our application down for a couple of hours, and have a team of engineers work during the late hours of Sunday evening to ensure the migration is completed successfully. 

First we updated our legacy Mongo database to the latest version by using a scripted approach that we tested during the previous week over and over again.

Next, we deployed the updated code, that was not compatible with the older database version and we did a "quick" 2 hour session of testing behind closed doors to make sure everything works as expected and the new code talks nicely with our new database.

We mitigated the risk of this failing by having a plan in place, just in case. We were prepared that if the migration would not be successfull we could easily revert to the older database version and push this job to the next weekend.

Fortunately this was not the case and the last step of the migration worked seamlessly so the entire public API was again exposed to the public and the mobile applications could again start to send traffic to our backend system.


