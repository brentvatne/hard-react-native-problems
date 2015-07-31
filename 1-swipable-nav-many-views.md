## Swipable navigation with many (20+) content-rich views

### In the wild

![](http://url.brentvatne.ca/18j8x.gif)

[Rugby League
Live](https://itunes.apple.com/us/app/rugby-league-live/id315297855?mt=8)

### Problems

- UITableView reduces view thrashing (destroying/re-creating) by re-use,
this isn't implemented in React Native.
- Eventually touch response becomes slow.

### Solutions

No good ones yet.
