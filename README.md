# Learn OpenUSD

## Resources

- [Learn OpenUSD](https://www.nvidia.com/en-us/learn/learning-path/openusd)
- [Introduction to USD](https://openusd.org/release/intro.html)
- [OpenUSD Viewer](https://docs.omniverse.nvidia.com/usd/latest/usdview/quickstart.html) 
- [OpenUSD Source Code](https://github.com/PixarAnimationStudios/OpenUSD)
- [OpenUSD API](https://openusd.org/release/api/index.html)
- [OpenUSD Q&A With Pixar’s Steve May | The Alliance for OpenUSD (AOUSD)](https://www.youtube.com/watch?v=YFwZSgwmAn4)
- [Book of USD](https://remedy-entertainment.github.io/USDBook/index.html)
- [ASWF Slack:](https://www.aswf.io/get-involved)
- [Alliance for OpenUSD (AOUSD) Forum](https://forum.aousd.org)
- [Nvidia Omniverse](https://www.nvidia.com/en-us/omniverse/)
- [da Vinci’s Workshop](https://docs.omniverse.nvidia.com/usd/latest/usd_content_samples/davinci_workshop.html)
- [ALab, Animal Logic](https://animallogic.com/alab/)

## Learn OpenUSD: Learning About Stages, Prims and Attributes

### Overview

- **Created and Manipulated USD Files:** Built and set up USD files from the ground up, establishing a strong foundation for 3D scenes.
- **Defined Primitives:** Defined various prim types, the fundamental elements of USD, and understood their significance within a 3D environment.
- **Established Scene Hierarchies:** Structured and organized 3D elements efficiently, creating a well-ordered and manageable scene hierarchy.
- **Lit Up Scenes:** Added dynamic lighting to scenes, bringing them to life and enhancing their visual depth.
- **Managed Attributes and Metadata:** Worked with attributes and metadata, setting, getting, and manipulating these essential elements to refine scenes.
- **Traversed and Inspected USD Files:** Navigated through USD files, examining and understanding the intricate details of the 3D scene data.
- **Verified Prims' Existence:** Checked the existence of specific prims to ensure the integrity and completeness of 3D scenes.

### Examples

- [01-create-usd-file.py](01-create-usd-file.py)
- [02-defining-cube-stage.py](02-defining-cube-stage.py)
- [03-creating-hierarchy.py](03-creating-hierarchy.py)
- [04-lighting-stage.py](04-lighting-stage.py)
- [05-adding-attributes-prim.py](05-adding-attributes-prim.py)
- [06-getting-value-current-attribute.py](06-getting-value-current-attribute.py)
- [07-traversing-stage.py](07-traversing-stage.py)
- [08-does-the-prim-exist.py](08-does-the-prim-exist.py)

### Content

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
    - Relationships enable robust encoding of dependencies and associations between scene elements, such as:
      - Binding geometry to materials
      - Grouping prims into collections
      - Establishing connections in shading networks
      - Modeling hierarchical relationships (e.g. parent-child)
    - Using relationships instead of hard paths enhances:
      - Non-destructive editing workflows
      - Referencing and asset reuse across tools
      - Collaborative workflows across teams

- **Primvars** address the need to "bind" user data on geometric primitives that becomes available to shaders during rendering. Some examples include, texture coordinates, vertex colors, or custom metadata, allowing for interpolating data on individual objects. Primvars are essential for various tasks, including:
  - Storing UVs for texture mapping.
  - Defining vertex colors for per-Vertex shading.
  - Deformation and animation.

- **XformCommonAPI** provides the preferred way for authoring and retrieving a standard set of component transformations, including scale, rotation, scale-rotate pivot and translation.
  - `xform_api.SetTranslate((10.0, 20.0, 30.0))`
  - `xform_api.SetRotate((45.0, 0.0, 90.0), UsdGeom.XformCommonAPI.RotationOrderXYZ)`
  - `xform_api.SetScale((2.0, 2.0, 2.0))`

- **Stage traversal** enables navigation and manipulation of the scenegraph.
  - `stage.Traverse()`

## Learn OpenUSD: Working With Prims and Default Schemas

### Overview

- **Define prims.** Start with the basics by learning how to define various types of prims, setting the stages for our 3D creations. Understand the role and significance of different prim types within a scene.
- **Retrieve prims by path.** Gain the ability to locate and retrieve prims using their specific paths, enabling precise control and manipulation of scene elements.
- **Validate prims.** Ensure the integrity of our 3D scenes by learning how to check if prims are valid. This step is crucial for maintaining a well-structured and error-free scene.
- **Set a default prim.** Discover how to designate a default prim for USD files, simplifying the management and navigation of complex scenes.
- **Understand USD API vs. schema-based API.** Explore the differences between using the USD API and the schema-based API, and understand when and why to use each approach for optimal results.

### Examples

- [09-defining-prim-without-schema.py](09-defining-prim-without-schema.py)
- [10-getting-validating-and-setting-prims-path.py](10-getting-validating-and-setting-prims-path.py)
- [11-setting-default-prim.py](11-setting-default-prim.py)
- [12-usdgeom-and-xform.py](12-usdgeom-and-xform.py)
- [13-scope-and-cube.py](13-scope-and-cube.py)
- [14-usdshade-and-material.py](14-usdshade-and-material.py)
- [15-usdlux-and-distantlight.py](15-usdlux-and-distantlight.py)

### Content