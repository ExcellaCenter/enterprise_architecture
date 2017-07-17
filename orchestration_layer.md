Orchestration Layer

Assumptions:
Many of the transactions in our applications are actually orchestrations of several Commands as well as other resources, such as logging, caching, SQL calls, and error handling. Since these workflows can be very consistent across apps an Orchestration Layer could be implimented so that the applications can interact with Business Objects rather than individual Commands and best practices can be aheared to throughout the enterprise.

Goal:
- consitant workflows and best practices across the enterprise
- code reuse when data is used in the same manner
- minimal impact to other apps when a change is made
- an explicit way to quickly know which apps will be affected by required changes.
- the flexibility to make App specific changes to a business object without affecting other apps.

Recommendation:
- This layer is where a data workflow for each Business Object, for instance the i-90, would be fleshed out and orchestrated.  - To minimize the impact of code resuse each Business Object in this Orchestration Layer would be split out as a seperate Gem allowing only apps which use the Business Object to depend on it.
- To allow for App specific changes and make it explicit which Apps are using a particular Business Object, Apps will not interact with a Business Object directly. 
- Instead, there will a local transform layer which can act as a pass through. (example: i90:digital_forms:save() which can map straight through to i90:save()) this will explicity show developers apps would be affected by a change and a place where tests could be wrapped.
- This local transform layer will also contain App specific data changes, allowing developers a place to make App specific changes while assuring that they will not affect other Apps.
