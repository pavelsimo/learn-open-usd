# Learn OpenUSD

## Resources

### Learning & Documentation
- [Learn OpenUSD](https://www.nvidia.com/en-us/learn/learning-path/openusd)
- [Introduction to USD](https://openusd.org/release/intro.html)
- [Book of USD](https://remedy-entertainment.github.io/USDBook/index.html)
- [OpenUSD API](https://openusd.org/release/api/index.html)
- [How to Use OpenUSD](https://developer.nvidia.com/blog/how-to-use-openusd/?ncid=so-link-523028)

### Tools & Source Code
- [OpenUSD Viewer](https://docs.omniverse.nvidia.com/usd/latest/usdview/quickstart.html)
- [OpenUSD Source Code](https://github.com/PixarAnimationStudios/OpenUSD)
- [Try NVIDIA NIM APIs](https://build.nvidia.com/explore/discover)

### Community & Forums
- [ASWF Slack](https://www.aswf.io/get-involved)
- [Alliance for OpenUSD (AOUSD) Forum](https://forum.aousd.org)
- [NVIDIA-Omniverse Forums](https://forums.developer.nvidia.com/c/omniverse/300?page=1)
- [NVIDIA-Omniverse Discord](https://discord.com/invite/nvidiaomniverse)

### NVIDIA Omniverse Ecosystem
- [Nvidia Omniverse](https://www.nvidia.com/en-us/omniverse/)
- [da Vinci’s Workshop](https://docs.omniverse.nvidia.com/usd/latest/usd_content_samples/davinci_workshop.html)
- [ALab, Animal Logic](https://animallogic.com/alab/)
- [NVIDIA-Omniverse GitHub](https://github.com/NVIDIA-Omniverse)
- [NVIDIA-Omniverse Documentation](https://docs.omniverse.nvidia.com/)
- [NVIDIA Omniverse - Learn With Me Streaming Series](https://forums.developer.nvidia.com/t/resources-from-the-learn-with-me-streaming-series/304680)
- [NVIDIA-Omniverse YouTube](https://www.youtube.com/c/nvidiaomniverse)

### Video Tutorials & Demos
- [OpenUSD Q&A With Pixar’s Steve May | The Alliance for OpenUSD (AOUSD)](https://www.youtube.com/watch?v=YFwZSgwmAn4)
- [Generative AI-Powered Virtual Factory Solutions With OpenUSD](https://youtu.be/cqggH5skWH8?t=3115)
- [Build Your First Omniverse Extension with OpenUSD](https://www.youtube.com/watch?v=pztkN1RFLKU)
- [OpenUSD 101 for Beginners | Learn With Me](https://www.youtube.com/watch?v=SPbnnSxAyKw)
- [OpenUSD and Physical AI Highlights from CES 2025](https://www.youtube.com/watch?v=Kte9EQ05BPk)
- [Building Operational Digital Twins Using IoT Data in OpenUSD](https://www.youtube.com/watch?v=NmfJJaN5uEE)
- [A “Simulation First” Approach to Developing Physical AI-Based Robots With OpenUSD](https://www.youtube.com/watch?v=pztkN1RFLKU)
- [Using NVIDIA Cosmos World Foundation Models for Physical AI Development](https://www.youtube.com/watch?v=wjCVFfmsai0)


## Learn OpenUSD: Learning About Stages, Prims and Attributes

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

- Examples:
  - [01-create-usd-file.py](01-create-usd-file.py)
  - [02-defining-cube-stage.py](02-defining-cube-stage.py)
  - [03-creating-hierarchy.py](03-creating-hierarchy.py)
  - [04-lighting-stage.py](04-lighting-stage.py)
  - [05-adding-attributes-prim.py](05-adding-attributes-prim.py)
  - [06-getting-value-current-attribute.py](06-getting-value-current-attribute.py)
  - [07-traversing-stage.py](07-traversing-stage.py)
  - [08-does-the-prim-exist.py](08-does-the-prim-exist.py)

## Learn OpenUSD: Working With Prims and Default Schemas

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
- Examples:
  - [09-defining-prim-without-schema.py](09-defining-prim-without-schema.py)
  - [10-getting-validating-and-setting-prims-path.py](10-getting-validating-and-setting-prims-path.py)
  - [11-setting-default-prim.py](11-setting-default-prim.py)
  - [12-usdgeom-and-xform.py](12-usdgeom-and-xform.py)
  - [13-scope-and-cube.py](13-scope-and-cube.py)
  - [14-usdshade-and-material.py](14-usdshade-and-material.py)
  - [15-usdlux-and-distantlight.py](15-usdlux-and-distantlight.py)


## Learn OpenUSD: Using Attributes

- There are two types of properties: attributes and relationships.
- To retrieve the properties of a prim, we would use the `GetProperties` method. 
- **Attributes** are the most common type of property authored in most USD scenes.
- We interact with attributes through the [UsdAttribute API](https://openusd.org/release/api/class_usd_attribute.html).
- **Custom attributes** in OpenUSD are used to define additional, user-specific properties for objects within a 3D scene. These attributes extend beyond the standard properties like position, rotation, and color, allowing creators to add unique data relevant to their specific needs. For example, custom attributes can store information such as material properties, animation controls, or metadata for a particular workflow.
  - For custom attributes that are not apart of any schema, we use the `CreateAttribute()` method.
  - `box_prim.CreateAttribute("weight_lb", Sdf.ValueTypeNames.Float)`
  - [Attributes Types](https://openusd.org/release/api/sdf_page_front.html#sdf_metadata_types)
- **Value resolution** is the algorithm by which final values for properties or metadata are compiled from all sources. 
  - You can use value resolution for resolving metadata using ``UsdObject::GetMetadata``.
  - For example, value resolution can be used in a product design or VFX workflow, where you often have multiple teams working on various aspects of a scene, to seamlessly combine data from multiple sources into a single model without overwriting work .
  - Another example can be illustrated with a robot arm model defined in two layers:
    - The base layer specifies the robot arm’s default properties, such as its position (0, 0, 0).
    - The operational layer contains overrides for when the robot arm is in use, changing its position to (5, 0, 0).
    - During value resolution, the final scene integrates these layers, resulting in the robot arm being positioned at (5, 0, 0), reflecting its operational state while retaining unchanged attributes from the Base Layer.
  - Understanding value resolution is key to working effectively with OpenUSD's non-destructive data modeling capabilities.
- **Metadata** is stored separately from the primary data and can be accessed and modified independently. It is typically used to store additional information that is not directly related to the geometry or rendering of an object, such as:
  - Author information
  - Creation/modification dates
  - Project-specific data
  - Annotations or notes
  - Rendering hints or flags
  - Metadata can be set at different levels of the scene hierarchy, allowing for both global and localized metadata.
- While both metadata and attributes allow us to store additional data, there are some key differences:
  - Metadata is separate from the core schema and data model, while attributes are part of the schema definition.
  - Metadata is typically used for supplementary information, while attributes are often used for data directly related to the object's properties or behavior.
  - Metadata cannot be sampled over time, allowing it to be evaluated and stored more efficiently than attribute values.
- Why use attributes over metadata?
  - If the value needs to be sampled over time, we would use attributes.
- **Custom attributes** in OpenUSD are user-defined properties that can be added to prims (the basic building blocks in OpenUSD) to store additional data.
  - Allow users to extend the functionality of OpenUSD at runtime to suit their specific requirements.
- **Schema attributes** in OpenUSD are predefined and standardized.
- **Custom schemas vs. Custom attributes**: When considering custom attributes versus custom schemas, the main strengths of custom attributes are their ease of use, and ability to be defined at any time, by any type of user. The main strengths of custom schemas are their ability to group related information, and provide standardization.
- **Custom attributes** are created and managed using the USD API. They can hold various types of data, such as numeric values, strings, or arrays, and can be sampled over time. This flexibility makes them useful for a wide range of applications, from simple metadata storage to complex animations.
  - Here are a few ways we can use custom attributes to enhance our OpenUSD workflows:
    - Metadata storage: Storing additional information about a prim, such as author names, creation dates, or custom tags. 
    - Animation data: Defining custom animation curves or parameters that are not covered by standard schema attributes.
    - Simulation parameters: Storing parameters for physics simulations or other procedural generation processes. 
    - Arbitrary end user data: Because they can be easily defined at run time, custom attributes are the best way to allow end users to define arbitrary custom data.
  - **Custom attributes** are the easiest and most flexible way to adapt OpenUSD to specific workflows and requirements, making it a powerful tool for industries like manufacturing, product design, architecture, and engineering, wherever we have multiple data types from many sources with varying purposes – like connecting our OpenUSD to sensor data or IoT for live, connected digital twins, or creating a production model with attributes like part numbers, manufacturer, life cycle costs, and even carbon data that can sync 3D scene description to 2D project documents, like a bill of materials or carbon emission calculators.
- Examples:
  - [16-retrieving-properties-prim.py](16-retrieving-properties-prim.py)
  - [17-getting-values-for-attributes.py](17-getting-values-for-attributes.py)
  - [18-authoring-attributes.py](18-authoring-attributes.py)
  - [19-create-additional-attributes.py](19-create-additional-attributes.py)
  - [20-modifying-attributes.py](20-modifying-attributes.py)

## Developing an Omniverse Kit-Based Application

- **.kit** An Omniverse application is defined by a .kit file, a text file that references all the application’s extensions and settings.
- **Kit App Template** repo is located at: https://github.com/NVIDIA-Omniverse/kit-app-template
- **Menu extensions**
  ```
  "omni.kit.menu.create" = {} # Create menu
  "omni.kit.menu.edit" = {}  # Edit menu
  "omni.kit.menu.file" = {}  # File menu
  ```
- **Windows extensions**
  ```
  "omni.kit.window.console" = {}  # Console/log
  "omni.kit.window.content_browser" = {} # Add content browser to UI
  "omni.kit.window.property" = {} # Property editor window
  "omni.kit.window.stage" = {}  # Stage tree
  "omni.kit.window.status_bar" = {}  # Status Bar
  "omni.kit.window.toolbar" = {}  # Manipular Toolbar
  ```
- **Extensions** are isolated units of application functionality defined via either Python or C++ code. Extensions that serve as the building blocks of Omniverse Kit-based applications.
  - An application, on startup, references the list of extensions in its .kit file and loads those extensions as part of the application’s appearance and functionality.
  - Each template places several extensions in its .kit file to provide a baseline of functionality, with the expectation that developers will add additional extensions to build out a custom application.
  - In your application’s .kit file, extensions are listed in the `[dependencies]` section. 
  - Adding an extension is as simple as adding a line of code at the end of the `[dependencies]` list. 

## How to Build OpenUSD Applications for Industrial Digital Twins

- **Digital twins** are primarily used in three key areas:
  - **Planning:** Enable real-time visualization and decision making during design, construction and commissioning phases. 
  - **Simulation:** Simulate design and operations to test for optimal production and material flow, ergonomics, and safety. AI and robotics developers can train and test the AIs and robotics that run in the real-world environment.
  - **Operations:** Integrate real-time production data to monitor, analyze, and resolve operational issues efficiently.
- **Creating a digital twin application** involves handling various data types and processes.
  - **3D data**:  
    - Do your users have existing data in different CAD tools?
    - Can they get 3D assets from manufacturers? Check with the manufacturers of real-world assets to see if they have CAD representations of their products.
    - Will your users need to scan some assets or create them in-house? They might need to work with a partner to obtain these assets. 
    - How will your users convert the assets to OpenUSD? See the Data Exchange options for more information.
  - **Robotics:** What kinds of data can you collect about operations, robotics, and automation processes within the environment? Find out as much as you can about these operations, and determine which data will need to be captured and utilized. 
  - **Real-time**, historical, or synthetic data: Which kind will it be? Determine the type of data you want to prioritize and visualize, where it will come from, and what format it will arrive in.
  - **Data integration process:** What is your simplest or most important use case?  Start with a data integration plan for that use case, and get it working before adding complexity. The Omniverse platform provides samples for [integrating CSV files and broker-based](https://github.com/NVIDIA-Omniverse/iot-samples) data into Kit-based applications, but you will need to customize these samples or create one of your own.
-  **Variants** OpenUSD can store multiple variations of assets, with VariantSets made up of two or more opinions. Variants make it possible for stakeholders to review different assets, materials, and asset placement within a single USD file.
- [**Measure Tool Extension**](https://docs.omniverse.nvidia.com/extensions/latest/ext_measure-tool.html) can be used to query for distances between objects with a variety of options. It is also possible to determine staggered distances, angles and areas.
- **Markup Extension** includes functionality for adding comments during review sessions. Let's look at some of its default functionality. 
- **Waypoint Extension** reviewers can save views of the scene and return to them later.
- **Section Extension** places an infinitely large section plane that visually cuts through assets.
- **PhysX extension** allows to simulate real-world behaviors based on physics, allowing us to optimize equipment layout, anticipate maintenance needs, train robots for tasks like pick-and-place or collision avoidance, and more.
  - ```"omni.physx.bundle" = {}```
- **NVIDIA Assets** the assets provided by NVIDIA are SimReady assets, which means each is built to real-world scale, with a Z-up pivot point placed and aligned so the asset “sits” properly with respect to the ground plane. Real-world scale is very important to an accurate physics simulation.
- **A Rigid Body** in a physics simulation, is an object that can move and collide with other objects, but which keeps its shape (doesn’t bend, squash, etc.) during a collision.
  - When a rigid body is **Kinematic Enabled**, the simulation acts like the body is continuously moving, and imparts that movement to other objects that it comes in contact with (in this case, the boxes).
- **Accurate physics simulations** can have various use cases in digital twins such as movement of products or parts, robotics simulations, sensor simulation, breakage scenarios, and fluid simulations.
  - See the [Simulation](https://docs.omniverse.nvidia.com/extensions/latest/ext_simulation.html) documentation.
- [IoT Samples](https://github.com/NVIDIA-Omniverse/iot-samples)
  - Connect IoT data sources (CSV, message broker etc.) to Omniverse
  - Incorporate IoT data in the USD model
  - Visualize IoT data, using an OmniUI extension
  - Perform transformations of USD geometry using IoT data
  - Incorporate Omniverse OmniGraph/ActionGraph with IoT data

## How to Build a Native OpenUSD XR Application

- [Bringing RTX to OpenUSD: Ultra-Realistic Spatial Experiences From the Cloud](https://www.nvidia.com/en-us/on-demand/session/siggraph2024-sigg2405/)

- **XR Extensions**
  ```
  "omni.kit.xr.example.usd_scene_ui" = {}
  "omni.kit.xr.core" = {}
  "omni.kit.xr.ui.config.metaquest" = {}
  "omni.kit.xr.profile.tabletar" = {}
  "omni.kit.xr.profile.vr" = {}
  "omni.kit.xr.profile.ar" = {}
  ```



## Getting Started: Simulating Your First Robot in Isaac Sim

- **URDF (Unified Robot Description Format)** is an XML-based file format used to describe the physical configuration of a robot. It includes details about the robot's links, joints, geometry, and physical properties like mass and inertia.

