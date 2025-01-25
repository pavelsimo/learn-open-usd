# Learn OpenUSD

## Basics

- **Stage**: represents the scenegraph, which dictates what is in our scene. It is the hierarchy of objects, called prims. These prims can be anything from geometry, to materials, to lights and other organizational elements. This scene is commonly stored in a data structure of connected nodes, which is why we refer to it as the scenegraph.

- **Composition**: composition is the result of the algorithm for how all of the USD files (or layers, in USD parlance, as USD content need not be file-backed) should be assembled and combined.

- **Hydra**: Hydra is a rendering architecture within OpenUSD that bridges scene data and rendering backends.
   - It operates on a scene delegate and enables render delegate plugins to generate rendering instructions for specific backends.
   - Hydra supports various rendering backends and techniques, including rasterization and ray tracing.
   - It provides extensibility through plugins and custom rendering backends:
     - **HdStorm**: is a real-time OpenGL/Metal/Vulkan render delegate leveraged by usdview.
     - **HdTiny**
     - **HdEmbree**
   
- **USD (.usd)** file can be either ASCII or binary – the advantage of which is that we can change the underlying format at any point without breaking references.

- **USDA (.usda)** are ASCII text files that encode scene descriptions in a format that can easily be read and edited.
  -  It is human-readable, which makes USDA particularly useful for tasks that involve manual editing or inspection of scene data.

- **USDC (.usdc)** is a compressed binary file format used by OpenUSD to store and exchange 3D scene data.
  - The Crate Binary Format uses various compression techniques to reduce the file size and improve loading performance.
  - The structure of the file is organized in a way that allows for efficient parsing and retrieval of the scene data.

- **USDZ (.usdz)** is an atomic, uncompressed, zipped archive so that we can deliver all of the necessary assets together. We would not use USDZ if we are still making edits to the asset, but it is a great way to package and ship our asset when it is complete.
  - For example, a mesh with its texture files can be delivered as one archive.
  - It’s generally intended as read-only and is optimal for XR experiences.

- **Prim** (Primitives) is the core component within the USD framework. Think of a prim as a container that holds various types of data, attributes, and relationships which define an object or entity within a scene. Prims can be of type: 
  - Imageable:
    - Mesh
    - Light
    - Xform
    - Skeleton
  - Non-imageable:
    - Material
    - Shader
    - Skeletal Animation

- **Scope** is a special type of prim that is used primarily as a grouping mechanism in the scenegraph. Think of scope as an empty folder on your computer where you organize files; similarly, scope helps in structuring and organizing prims within a USD scene.

- **Xform** is a type of prim that stores transformation data, such as translation, rotation, and scaling, which apply to its child prims. This makes xforms a powerful tool for grouping and manipulating the spatial arrangement of objects in a 3D scene. Xform stands for 'transform', reflecting its role in transforming the space in which its children reside. Typical use cases include: 
  - animating characters
  - robotic arms: where different parts are children of an xform prim. 
  - arranging furniture in architectural visualization: where all items in a room might be scaled or rotated together. 

- **USD code repository** consists of four core packages:
  - **base** (Package)
  - **usd** (Package)  
    - **Usd** (Module):  
      The core client-facing module for authoring, composing, and reading USD. It provides an interface for creating or opening a Stage, as well as generic interfaces for interacting with prims, properties, metadata, and composition arcs.  
      - **UsdGeom** (Schema Module)
      - **UsdShade** (Schema Module)
      - **UsdLux** (Schema Module)
    - **Sdf** (Module):  
      The Scene Description Foundation provides the core functionality for serializing scene description into a reference text-based file format and implements scene description layers (SdfLayer), which store parts of the scene description. This module is commonly used for managing prim and property paths and creating USD layers.
    - **Gf** (Module):  
      The Graphics Foundation contains essential classes and functions that support graphics, including linear algebra, basic mathematical operations, and basic geometry. This module provides the classes for 3D data types that are used for getting and setting particular USD attributes.
  - **imaging** (Package)
  - **usdImaging** (Package)

- **USDLux** is a set of light types and light-related schemas. It provides a standardized way to represent various types of lights, such as:
  - Directional lights (UsdLuxDistantLight)
  - Area lights, including
  - Cylinder lights (UsdLuxCylinderLight)
  - Rectangular area lights (UsdLuxRectLight)
  - Disk lights (UsdLuxDiskLight)
  - Sphere lights (UsdLuxSphereLight)
  - Dome lights (UsdLuxDomeLight)
  - Portal lights (UsdLuxPortalLight)

- **Properties** are used to describe the characteristics of objects, or "prims," within a USD scene. There are two types of properties:
  - **Attributes** store data values that define the appearance, behavior, or other properties of a prim.
    - Attributes are values with a name and data type that define the properties of prims in a USD scene. 
    - Attributes are the primary means of storing data in USD. 
    - Each attribute has a single, defined data type.
    - Attributes are authored and stored within USD layers, enabling efficient scene composition.
    - Attributes can be animated by providing key-framed values over time.
    - They can be queried, modified and animated using the USD API.
    - Examples:
      - Visibility - Controls the visibility of a prim in the scene.
      - Display color - Specifies the display color applied to a geometric prim.
      - Extent - Defines the boundaries of a geometric prim.
  - **Relationships** on the other hand, establish connections between prims, enabling hierarchical structures and data sharing. 

## Resources

- [Learn OpenUSD](https://www.nvidia.com/en-us/learn/learning-path/openusd)
- [Introduction to USD](https://openusd.org/release/intro.html)
- [OpenUSD Viewer](https://docs.omniverse.nvidia.com/usd/latest/usdview/quickstart.html) 
- [OpenUSD Source Code](https://github.com/PixarAnimationStudios/OpenUSD)
- [OpenUSD API](https://openusd.org/release/api/index.html)