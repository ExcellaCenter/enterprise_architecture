Command Layer

Assumptions:
Transactions with an external resource should be very consistent.  Since external resources shouldn't change regularly, it makes sense abstract these details.  However, although most of our apps rely on external resources, they don't always rely on the same external resources and changes should affect as few apps as possible.

Goal:
- Consistent transport logic and error logging.
- Code reuse while minimizing the impact of changes.

Proposal:
- Implement a Command Layer to encapsulate transactions with external resources.
- Each individual Command would be a one to one representation of an external API point. 
- Split this Command Layer in to multiple gems to minimize the impact of code changes.
- At a minimum, the Command Layer should be split up by end point; arguments could also be made to split it up by concern within an end point.
- Apps would not reach out to Commands directly, instead, they would access Commands through the Orchestration Layer.
