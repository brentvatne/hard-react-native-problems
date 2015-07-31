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

None yet.

### Unimplemented Ideas

#### Destroy/create views on the fly (by @paramaggarwal)

Current `ListView` implementation is memory heavy and cheap on processing. There is an alternative which is memory light, but processing heavy. `ListView` exposes a method `onChangeVisibleRows`. Using this data, it is possible to keep track of rows on screen. Also each row has an `onLayout` method which gives the final top, left, width, height of the cell.

To make both of these work together, store the data from `onLayout` on the component and then pass whether the row is visible as a prop. Then show the actual cell `if (this.props.isVisible || !this._layoutMeasurement)` - that is render the complete view if it is visible or the first time layout has not completed. If the layout data is available, and the row is off-screen then simply render an empty `View` with the width and height from the layout data.

This is not completely infinite as there is still an empty `View` for each row. You can use `removeClippedSubviews` property of `ListView` to not add native views to the heirarchy when they are offscreen.

#### Wrap UITableView/UICollectionView (by @paramaggarwal)

To get reusability with `UITableView` and `UICollectionView`, React's reconciliation algorithm actually fits for taking a dirty view as input and getting a correctly configured view out.

Imagine every time a new cell is rendered by React - it will give it a unique `react-id`. There is a corresponding virtual view node with React. When later at some point we get this dirty node back, we fetch the virtual view node corresponding with the `react-id` and then we diff it with what we actually want and hence we can manipulate that cell to what we want with the minimum number of changes.

Now `UITableView` and `UICollectionView` expect this to happen synchronously. So we can return an empty `View` immediately with the width and height that we already know from our virtual view node. Then using the ideas from AsyncDisplayKit we asynchronously do the diffing and update the dirty cell into what we actually want.
