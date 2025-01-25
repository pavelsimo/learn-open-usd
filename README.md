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
- [NVIDIA-Omniverse GitHub](https://github.com/NVIDIA-Omniverse)
- [NVIDIA-Omniverse Forums](https://forums.developer.nvidia.com/c/omniverse/300?page=1)
- [NVIDIA-Omniverse Discord](https://discord.com/invite/nvidiaomniverse)
- [NVIDIA-Omniverse Documentation](https://docs.omniverse.nvidia.com/)
- [NVIDIA-Omniverse YouTube](https://www.youtube.com/c/nvidiaomniverse)

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

- **Define prims.** Defines various types of prims, which serve as the building blocks for 3D creations. Also covers the importance of different prim types within a scene.  
- **Retrieve prims by path.** Locates and retrieves prims using their specific paths, enabling precise control and manipulation of scene elements.  
- **Validate prims.** Ensures the integrity of 3D scenes by checking the validity of prims, a crucial step for maintaining well-structured and error-free environments.  
- **Set a default prim.** Designates a default prim for USD files, simplifying the management and navigation of complex scenes.  
- **Understand USD API vs. schema-based API.** Explores the differences between the USD API and the schema-based API, highlighting when and why to use each approach for optimal results.

### Examples

- [09-defining-prim-without-schema.py](09-defining-prim-without-schema.py)
- [10-getting-validating-and-setting-prims-path.py](10-getting-validating-and-setting-prims-path.py)
- [11-setting-default-prim.py](11-setting-default-prim.py)
- [12-usdgeom-and-xform.py](12-usdgeom-and-xform.py)
- [13-scope-and-cube.py](13-scope-and-cube.py)
- [14-usdshade-and-material.py](14-usdshade-and-material.py)
- [15-usdlux-and-distantlight.py](15-usdlux-and-distantlight.py)

### Content

- **Specifiers** n OpenUSD convey the intent for how a prim or a primSpec should be interpreted in the composed scene. The specifier will be one of three things: 
  - **Def** which is short for define, defines the prim in the current layer. 
  - **Over** which is short for override, holds overrides for opinions that already exist in the composed scene on another layer.
  - **Class** prims are essentially a blueprint. They contain opinions that are meant to be inherited, making it useful when you’re creating base prims from which other prims can inherit properties or opinions.
  ```usd 
  # Indicates that box is fully described as a Cube prim in the stage, with a size property set to 4. 
  def Cube “Box” {
      double size = 4
  }
  
  # The over specifier modifies the size property without redefining it entirely; in this case, size is overriden to have a value of 10. This change only applies to this specific instance; it does not redefine the prim at the root level. 
  over “Box” {
      double size = 10
  }
  
  # Defining a new prim as a class called "_box". This can be used as  a reusable template in the USD scene. 
  class “_box” {
      double size = 4
  }
    ```
- **Path** is a type that represents the location of a prim within a scene hierarchy. Its string representation consists of a sequence of prim names separated by forward slashes (/), similar to file paths in a directory structure. The stage root, which serves as the starting point for the hierarchy, is represented by a forward slash ("/"). 
  - **Sdf.Path** objects in OpenUSD provides a way to uniquely identify and locate objects (prims) within our scene hierarchy. 
  - `box_prim: Usd.Prim = stage.GetPrimAtPath("/box")`

- `Default prim` is a top-level prim, or primitive, that is part of the scene’s metadata and serves as the primary entry point or root for a stage. Think of it as the “control point” in the scene, which helps other parts of the system know where to start or what to focus on. 
  - It is best practice to set a default prim in our stages. This is crucial for tools and applications that read USD files, as it guides them to the primary content; for some it may even be considered invalid if the default prim is not specified for the stage.
  - **usdchecker** checks for a default prim and reports an error if it is not set on a stage. A default prim is also particularly useful when the stage’s root layer is referenced in other stages (such as a reference or payload), as it eliminates the need for consumers to specify a target prim manually.
  - The defaultPrim metadata is set to Car, indicating that Car is the main entry point of this USD file. When we bring this .usda in as a reference or payload the Car will show up visually in the stage.
  ```usd
  #usda 1.0
  (
      defaultPrim = "Car"
  )
  
  ...
  ```
  
- **Schemas** serve as blueprints that author and retrieve data, like attributes and  relationships that govern behaviors of objects in a USD scene. They provide a consistent and extensible way to define and interpret data, ensuring data interoperability between different software tools and applications.
  - While schemas define the structure and rules, they do not necessarily include the implementation of behaviors. For example, the UsdPhysics schema does not come with a physics engine.
  - There are two types of schemas:
    - **IsA schemas** also known as Typed schemas or Prim schemas, essentially tell a prim what it is. Because of this, each prim can only subscribe to one IsA schema at a time.
      - **UsdGeom** defines schemas for representing geometric objects, such as meshes, cameras, and curves.
      - **UsdLux** defines schemas for representing light sources in a scene. It includes schemas such as sphere lights, disk lights, and distant lights.
    - **API schemas** are similar to IsA schemas except it does not specify a typeName. Since it does not have a typeName they are considered to be non-concrete. API schemas can be applied to prims to add specific properties that govern behaviors, such as adding rigid body capabilities to an object hierarchy. 
      - **UsdPhysics** adds physics properties to any UsdGeomXformable object for simulation such as rigid body dynamics.
      ```usd
      # Import related classes
      from pxr import UsdPhysics
  
      # Apply a UsdPhysics Rigidbody API on the cube prim
      cube_rb_api = UsdPhysics.RigidBodyAPI.Apply(cube.GetPrim())
      
      # Get the Kinematic Enabled Attribute 
      cube_rb_api.GetKinematicEnabledAttr()
      
      # Create a linear velocity attribute of value 5
      cube_rb_api.CreateVelocityAttr(5)
      ```

