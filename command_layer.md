Command Layer

Proposals:
- Each seperate external end pould have it's own Command Gem.

Questions:
- Would services that know about more than one command live in these gems, or in apps that depend on them?

Drawbacks:
- Versioning a gem is one more step than versioning code that's contained in the app. A developer modifying the command gem might would have do at minimum 2 pull requests to affect the user facing website: One to modify the gem, and one to tell the gem's dependents to depend on a later version of the gem. In general, I think having a command gem to wrap each external endpoint isn't a bad idea, but I think Reena will point out the longer developer workflow as a drawback of this approach. 
