## Hard React Native Problems

This repository is intended to house a list of examples of functionality
from native apps that seem hard to implement (performantly or at all)
with React Native, so that the community can attempt to find solutions
and, when necessary, provide real-world examples to guide API design for
any changes to core or new libraries that make the solutions easier.

#### Please, add your example problems to this project!

Fork this project, update the README to add an example.


#### What you should do with this

Try your hand at a solution! Create a repository for it, and submit a
pull request with a link to it under the solutions section of the
problem that you are trying to solve. Discuss possible solutions in the
issues.

### 1) Swipable tabbed navigation with many (20+) content-rich views

#### In the wild

![](http://url.brentvatne.ca/18j8x.gif)

#### Problems

- UITableView reduces view thrashing (destroying/re-creating) by re-use,
this isn't implemented in React Native.
- Eventually touch response becomes slow.

#### Solutions

No good ones yet.
