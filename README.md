# Outstanding Questions

What are the objective attributes that would make an architecture successful on this project?
Examples would be: code performance, scaleability, flexiblity, maintainablity, readability, code reuse, separation of concerns, fewer bugs, transparency of code impact, time to market of new features, time to resolution of maintaince issues, etc.

Knowing that many architectual decisions will impact two desireable attributes, which attributes would you be willing to sacrifice for gains in the opposite category?  (possible examples performance vs. readability, code resuse vs. change isolation)

(from Will):

I think that one of Reena's main concerns with shared dependency is developer workflow. If we have a gem with shared
models in it, we need to update the gem, and then update the `Gemfile.lock` in the app that depends on the gem, and this
means waiting on the pipeline twice and waiting on PRs to be approved twice. Therefore, I think we should recommend that
any **shared gem should consist only of things that rarely change**. 

The part of our recommendation that I am most attached to is the recommendation of layering: 

1. Commands wrap discrete external calls, e.g., `G28::CreateCaseCommand`. These commands are also responsible for error logging if external calls fail. 
2. Services orchestrate the action of several commands, and return models. If several commands need to be called in order to build or change a model, the service encapsulates this knowledge. 
3. Controllers and views know about services and models, but not about commands. 

Questions about this approach: 

1. Do purely internal models that are just active records need services or commands? I think for consistency in controllers, we should use services to access them, but the services need not use commands to talk to our own database. 
2. What should the call from a controller into a service look like? Is the controller making an API call, or a Ruby method call?
3. Do we have one app or gem with services in it, or do apps all have their own services, or a mix?
