# notes related to simulations and computer graphics

## basics

- computer-generated imagery (cgi)
  - creates still or animated visual content with computer software

- voxel
  - represents a value on a regular grid in three-dimensional space [^1]
  - typically don't encode their position (i.e. coordinates) explicitly with their values
  - rendering systems infer the position of a voxel based upon its position relative to other voxels

- voxel data formats: .vxl, .vox, .kvx, .kv6, .v3a, .v3b

- volumetric meshes
  - regular
  - irregular


## blender

- foss modeling software
- hotkeys
  - view
    - rotate around center: 	middle mouse
    - pan: 					shift + middle mouse


## unity3d

- simple compute shader in unity https://www.youtube.com/watch?v=BrZ4pWwkpto
- simulating ant colony using compute shaders https://www.youtube.com/watch?v=X-iSQQgOd1A


## generic compute [^2]

- computesharp https://github.com/Sergio0694/ComputeSharp
  - only works on windows 10
  - has the benefit of not needing any other dependencies (no need to install CUDA or OpenCL to get GPU support)
  - there is a Roslyn source generator that rewrites the shaders at build time from C# to HLSL (mapping types, 
    methods, intrinsics, etc.), then shaders are compiled and cached at runtime (this gives the library some 
    additional flexibility, like being able to have shader metaprogramming too, ie. capturing delegates in a 
    shader to compose them dynamically) and then dispatched on the GPU

- ilgpu https://github.com/m4rs-mt/ILGPU/
  - has backends for cuda/opencl/cpu


## collision detection

- types
  - static
    - faster
    - velocities are not taken into account, risk of tunneling
  - dynamic
    - slower
    - report exact time of collision and point of contact

- swept volume
  - the volume covered by an object in continuous motion over a specified time interval
  - if swept volumes of two objects dont intersect, there is no collision
  - speedbox - simplified approximation of swept volume, but doesn't have to be literally a box

- spatial partitioning
  - bounding volume hierarchies
  - bounding volumes
  - surface geometry
  - octree (quadtree for 2d)


## references

[^1]: https://en.wikipedia.org/wiki/Voxel
[^2]: https://news.ycombinator.com/item?id=26237968
