# Cargo

`AUTHOR: Idra`
`HAS CONTEXT: Idra`

Honestly just ask @Idra if any of this doesn't make sense because it is (by necessity) quite complicated.

## How it works

Cargo works by connecting together `PylonCargoBlock`s together using `CargoDuct`s. Cargo differs from fluids in that cargo ducts cannot have junction: each length of cargo duct connects together two endpoints.

## PylonCargoBlock

`PylonCargoBlock` represents a cargo endpoint. When a block implements `PylonCargoBlock`, it can add logistic groups (see `PylonLogisticBlock`) to faces, specifying the face type (INPUT or OUTPUT). When a logistic group is associated with a face and a type, cargo ducts can connect to that face.

## Item routing

A big problem in cargo ducts is that any part of a connection could be unloaded at a time, considering that connections can be practically infinitely long. This is practically very difficult when it comes to routing. We could just store in memory which endpoints are linked together with which nodes, but this store must then be updated whenever any update to the network occurs.

The simplest way I could find to solve this is with a cache. Whenever we want to find out what input an output is connected to, we consult the cache. If the cache has already computed a route, it is returned. Otherwise, we compute the route but starting at the output and following all the cargo ducts until we arrive at an input. All the cargo ducts are recorded. Whenever any block on the route is modified (broken or unloaded), the entire route is deleted and must be recalculated.

This means that if the middle section of a cargo duct network is unloaded, the route is invalidated and cargo will no longer be routed along that network.

## Cargo ticking

Each `PylonCargoBlock` periodically ticks. A cargo block tick looks like the following:

1) Iterate over every output face (and its corresponding logistic group) on the cargo block
2) Find the corresponding input block+face (if they exist) (and corresponding logistic group) using the cache as described above
3) Iterate every source slot in the source logistic group
4) Iterate every target slot in the target logistic group
5) Check if we can transfer items from the source slot to target slot (e.g. if the source contains some oak logs and the target contains nothing or also oak logs and less than 64 of them)
6) Hold on for dear life as your computer combusts
7) Once we manage to transfer any item or run out of source or target slots to iterate, we are finished

## CargoDuct

Cargo ducts keep track of their connected faces and manage their associated displays. That is basically their only function. Whenever a cargo block or cargo duct is placed next to them, they check if they can connect to that duct/block. If so, add it to the list of connected faces, refresh the item displays, and then also update the other block and refresh its item displays.

Item display refreshing mainly involves looking at all the connected faces, and ensuring each one has an associated display. (And also it deletes any displays which should no longer exist).

Also, there are events called when cargo ducts or blocks connect/disconnect.

## Cargo block hack

Cargo blocks do NOT keep track of the connected faces. 'What the f*ck do you mean?' you might say. 'Can cargo blocks not connect together directly, without needing a cargo duct in between?!' Yes, but it's a hack. Basically, when I route the item routing logic, it already worked for directly adjacent cargo blocks, so all I had to do was make the displays update correctly. I just created a function `updateDirectlyConnectedFaces` which basically just ensures that all of the displays are correct by checking all of the adjacent cargo blocks. The display that connects two cargo blocks together is actually owned by one of the specific cargo blocks (not all the cargo blocks, as with cargo ducts). It's just a big hack.

## Z-fighting

Caution must be taken to avoid Z-fighting. The displays that connect ducts together are actually all different widths, otherwise they would overlap and Z-fight. This is done by having 3 different widths and ensuring that when we connect two ducts together on one or two corners, the new display spawned between them is NOT any of the widths that the corner duct's existing display (if it exists) already use. Hopefully that made sense

