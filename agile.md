# Agile development

Brief walkthrough on *How We Work Agile with Rymd™*. Intended for use in project management apps like Pivotal Tracker and/or Trello, etc.

## Stories

A *User Story* is kind of like a feature in the system. It might be really high level, or on a more low level technical level – it's up to us on how we define them. 

A good story should ideally:

- **Represent a single feature in the system**. One should be able to refer to the story in the future, and connect it to a well defined feature in the system. 
- **Be practical and concrete**. I.e. no abstract stuff. It should be *doable* and *understandable* just by reading the title (or the description in worst case). If you can't form a story of a concept, consider breaking it down in smaller stories.
- **Be finishable**. When creating a story, ask yourself: "When is it considered 'Done'?". Write the answer in the description. 

### Syntax

We *should* write stories on the syntax:

	<Role> should be able to <do something in the system>

Example:

	User should be able to add a Resource

This is of course not doable in every singe case, but use it as an ambition. Note how objects in the domain are capitalized (such as *Resource*, *User*, *Node*).

### Ownership

A story has a *Requester* and an *Owner*:

- **The Requester** is the person who's created the story. 
- **The Owner** is the person who's assigned to the story (for the moment).

The requester acts as the client/customer, and the owner is the developer/deliverer in this scenario. It's the owner who can accept or reject the story (see *"Stages"* below).

A story isn't required to be owned by the same person throughout its lifetime – it may be assigned to another team member as progress is made.

## Pivotal Tracker

[Pivotal Tracker](http://pivotaltracker.com) is an agile management tool well suited for software development. It includes agile concepts like stories, owners, epics, backlog, sprints, etc.

### Stories, Bugs and Chores

In Pivotal a story may be of three different types: 

- **A Feature**: a regular feature story. A feature story is something that ideally creates value for the end user – something you can refer to and "touch".
- **A Bug**: well, it's a bug. Something that has gone wrong and should be fixed.
- **A Chore**: something in between a bug and feature. It's not something the end user sees, but it's neither an error. Just something that "should be fixed" or "has to be done" in order to proceed, i.e. "Set up PeerJS server".

### Story status

In Pivotal a story has different statuses:

- **Not started**. Nobody works on this.
- **Started**. A team member has started working on this story, and thus becomes the story's owner. Really important to mark, so the communication is clear on who's working on what.
- **Finished**. The story is finished by the owner.
- **Delivered**. The result of the story is published (ex. pushed to main repo or deployed to staging servers) for the requester to view.
- **Accepted/Rejected**. After the story is delivered the requester should be able to inspect the results and either accept or reject it. If the story is rejected, it may be restarted by the owner.

It's really important to keep the status of a story up to date.

### Icebox, Backlog and Sprints

When a story is created it's added to the *Icebox*. It means the story is "alive", but not prioritized (it's "out in the cold"). It's on the roadmap "sometime", just for memory's sake. 

A story is prioritized when it's moved from the icebox to the *Backlog*. Well there it can be prioritized by reordering.

The top of the backlog forms the current sprint – stories that are worked on right now. Make this realistic.

### Estimates

A story's complexity may be *estimated* by assigning it *points*. Points are not hours, but rather an abstract concept for the team itself to defined. Think of it like a scale on how hard a story is to finish.

### Epics

An *epic* is a way to connect and group similar stories, perhaps for a release or for a certain feature type. For example, a "Prototype 1" epic may be created in Pivotal, which collects all stories assigned with the tag `prototype 1`. This is a great way of keeping track of the progress of an area.

## General tips

- Keep the conversation going in the comments for a story.
- Feel free to refer to git commits in the comments or story description.
- Be concrete and hands on!
- Keep everything up to date. It's important when working remote.
- Written communication is important. Try to describe things as clear as possible.
