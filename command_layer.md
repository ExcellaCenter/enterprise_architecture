Command Layer

Goal:
Transactions with an external resource should be very consistent.  Since external resources shouldn't change regularly, it makes sense abstract these details into a command layer.  However, although most of our apps rely on external resources, they don't always rely on the same external resources.  The goal is to maximize code reuse while minimizing the impact of changes on the various services using the commands. 

Proposal:
- Implement a Command Layer to maximize code reuse for transactions with external resources.
- Each individual Command would be a one to one representation of 
- Split this Command Layer in to multiple gems to minimize the impact of code changes.
- At a minimum, the Command Layer should be split up by end point.  Arguments could be made to split it up by concern or the more extreme option, for a truly micro-service architecture, each Command could split into it's own Gem.
- Apps would not reach out to Commands directly, instead, they would access Commands through the Orchestration Layer.

Questions:
- Would services that know about more than one command live in these gems, or in apps that depend on them?

Drawbacks:
- Versioning a gem is one more step than versioning code that's contained in the app. A developer modifying the command gem might would have do at minimum 2 pull requests to affect the user facing website: One to modify the gem, and one to tell the gem's dependents to depend on a later version of the gem. In general, I think having a command gem to wrap each external endpoint isn't a bad idea, but I think Reena will point out the longer developer workflow as a drawback of this approach. 
