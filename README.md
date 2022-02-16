# bioverse-zones

I've always wanted biodiversity to be included when making travel plans. Whether selecting a hike, a place to go on vacation, or just somewhere for a drive I've wanted to be able to map out biodiversity. This kind of thing is a perfect counterpart to a field guide. Whereas a good field guide effectively obsfucates itself (you learn what's in the area and how to ID it on your own) a guide like this could keep point you to new places you don't yet know how to ID. So I decided this would be a nice addition to bioverse.

In summary the purpose of this is to provide an API that takes
- filters (conifers, birds, insects, etc)
- a region (whatever's being displayed on the map)
- a zoom level (represented by a h3 hex cell granularity) 

And returns zones to be plotted out on a map.

## Current Approach
- Creating zones is totally a clustering problem
- Distance between hex cells can be defined by an set difference (in terms of species)
- To avoid the issue of distance domination by hyper diverse taxa we can do a kind of "equal share" weight partitioning. The basic idea here is that for a specific level in the taxonomic tree, all splits below that level gain an equal portion of the current level's weight. So if you have a single species at the bottom of five splits it'd get a score of 1 where as if in another part of the tree each split resulted in 10 new lower nodes you'd have a score of 1/100000 for each resultant species. 
- We use average member distance to define the distance to a cluster (min results in strings of examples, max means clusters don't form on general likeness)
- Then we can simply chop our hierchy at a level that gives back a reasonable number of zones.

We'll see how this works! We'll start by doing this manually and then if it works out build an API and then incorporate the API into the app.
