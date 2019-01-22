---
layout: post
title: "Part I: Indexing Datasets of 3D Indoor Objects"
date: 2019-01-15 13:32:20 +0100
description: Cataloguing datasets of object models # Add post description (optional)
img:  # Add image post (optional)
---

This is the first part of a series of posts on consolidating datasets of 3D objects and scenes and in this post, we will focus on datasets of 3D objects. This is a modest attempt at covering the breadth of such datasets that have publicly appeared over the past one and a half decade. These datasets have been curated either via synthesising 3D models using a software or scanning real world 3D objects from multiple views with RGB as well as depth cameras. They have been immensely useful for object detection, segmentation and grasping among other applications. Historically, researchers in computer vision and graphics have maintained a particular interest in 3D shape modelling and understanding and therefore contributed to the growth and evolution of these datasets. Notably, there have been attepmts at curating datasets by the game development community but they have remained within the confines of the community and have largely not been publicly shared or released for free. It is worth mentioning that today various companies and websites (the list below only mentions a few popular ones and is by no means exhaustive) allow creating, sharing and searching 3D models *e.g.*

- [Onshape](https://www.onshape.com/) have a large repository of CAD models that are freely available for research purposes. They are a cloud based service for designing and sharing CAD models.
- [3DWarehouse](https://3dwarehouse.sketchup.com/?hl=en) maintain a large collection of 3D models created in sketchup and also provide a search engine for these. The 3D models can be downloaded for free.
- [Clara](https://clara.io/library), like onshape is a cloud based 3D content creation software and provides many 3D models for free.
- [Yobi3D](https://www.yobi3d.com/) allows searching 3D models and provide links to the corresponding website where those models can be available. Not all of them are for free.
- [Unity Asset Store](https://www.assetstore.unity3d.com/) provide 3D models that can be used within the Unity3D engine. High quality assets tend to require licensing and not available free of charge.
- [Kujiale](https://www.kujiale.com/), an indoor design platform in China that provides 3D indoor objects as well scenes but they are not available for free.

> It is important to note that even though these models are freely available, most commercial companies cannot simply use them. In most cases, special agreements have to be made via appropriate legal channels and departments to use them. Therefore, it is worthwhile spending time reading the license agreement file for any terms and conditions that may come with the dataset.

![](/assets/img/2019-01-15/object_repos_1.jpg){:width="70%"}


https://3dprintingforbeginners.com/3d-model-repositories/ 

https://www.aniwaa.com/best-sites-download-free-stl-files-3d-models-and-3d-printable-files-3d-printing/

### Data formats

#### CAD models
CAD design and modelling have a long history of enabling creation of 3D models of complicated objects on a computer. This has been extremely powerful in manufacturing, design and architectures of building and bridges. Right from the early days of revolutionary [Sketchpad](https://www.youtube.com/embed/YB3saviItTI) to today's cloud services for design, CAD modelling has evolved immensely. The image below shows the evolution of CAD.

[![](/assets/img/2019-01-15/The-history-of-CAD_CADENAS_R3.jpg)](/assets/img/2019-01-15/The-history-of-CAD_CADENAS_R3.jpg){:width="70%"}

CAD allows engineers and designers to build realistic computer models of parts and assemblies. These models can be then 3D Printed or CNC machined as well as used to run complex simulations. A wide range of parameters can be simulated such as strength or temperature resistance before any physical models have been created, enabling a much faster and cheaper workflow.

<img src="/assets/img/2019-01-15/onshape_design.gif" style="border: 0pt none; float:left; padding-right:10px; padding-bottom:10px" width="50%">CAD had its origins in three separate sources, which also serve to highlight the basic operations that CAD systems provide. The first source of CAD resulted from attempts to automate the drafting process. These developments were pioneered by the General Motors Research Laboratories in the early 1960s. One of the important time-saving advantages of computer modeling over traditional drafting methods is that the former can be quickly corrected or manipulated by changing a model's parameters. The second source of CAD was in the testing of designs by simulation. The use of computer modeling to test products was pioneered by high-tech industries like aerospace and semiconductors. The third source of CAD development resulted from efforts to facilitate the flow from the design process to the manufacturing process using numerical control (NC) technologies, which enjoyed widespread use in many applications by the mid-1960s. 

Similar to vector graphics for images, this representations allows resampling the surface data at arbitrary resolutions, with or without connectivity information (i.e. into a point cloud or a mesh). [GMSH](http://gmsh.info/) 3D dimensional finite element mesh generator --- converts parametric shapes to meshes. [This link](http://gmsh.info/screencasts/) shows how to use the software.



#### STL format
The format only describes the 3D surface geometry of the object *i.e.* information about 3D vertices and normals is provided and no information of colour, texture or other possible meta-data relevant for the model is included. These files are usually generated by a CAD program and are most commonly used in the 3D printing. They store the 3D information using a concept called "tessellation" where a primitive shape (*e.g.* a triangle described by three vertices and a normal) is repeated across to encode the surface geometry without overlaps and gaps. The format was invented by the _Albert Consulting Group_ for [3D systems](https://en.wikipedia.org/wiki/3D_Systems), a company co-founded by [Chuck Hull](https://en.wikipedia.org/wiki/Chuck_Hull), in 1987. Chuck had then invented stereolithographic 3D printer and his company were looking for a way to transfer the information from 3D CAD models to the printer and realised they could use the concept of "tessellation" to describe the geometry. For instance, the image below shows different levels of tessellation of sphere done with a triangle. 

<center><img src="/assets/img/2019-01-15/mesh_stl.jpg" width="60%"></center>

STL files come in two different flavours namely ASCII and Binary and contain descriptions of 3 vertex facets including their normals. The ordering of the vertices complies with the right hand rule. The main restriction placed upon the facets in STL files is that all adjacent facets must share two common vertices. 


#### OBJ format 

The OBJ format was created by [Wavefront Technologies](https://en.wikipedia.org/wiki/Wavefront_Technologies) to store lines, polygons, and free-form curves and objects. Similar to STL it stores the surface geometry but unlike STL it also stores the colour and texture information. OBJ format can approximate surface geometry without blowing up the size of the model using bezier curves or NURBS. There are multiple ways to store the geometry with OBJ format. In its simplest form, OBJ allows tessellation of the geometry in the form of triangles, quadrilaterals or more complext polygons. The vertices and normals of the polygons are stored to encode the geometry. Other ways to encode geometry with OBJ include free-form curves like bezier curves and free-form surfaces like NURBS. Free-form surfaces are more precise and they lead to smaller file sizes at higher precision compared to other methods. Although STL remains the most popular format for 3D printing, the size of the file very quickly increases for high-resolution 3D models and the lack of colour information makes it somewhat restrictive and therefore OBJ has been slowly gaining popularity.

<div><figure><img align="left" src="/assets/img/2019-01-15/texture_mapping.gif" width="25%"></figure> OBJ format supports colour and texture in an accompanying file with .MTL extension which allows the end-user to render a multi-coloured textured model. The MTL file encodes various intrinsic properties of object (<i>e.g.</i> ambient color, diffuse color, specular color, transparency etc.) as well as texture maps that allow mapping an image onto a 3D surface <i>e.g.</i> in the animation on the left, the 2D textured image is wrapped around the 3D cube where vertices of cube are projected on the 2D atlas and their colours are interpolated from the image. </div>

#### Other Formats

URDF image https://gkjohnson.github.io/urdf-loaders/unity/Assets/URDF-Loader/


### Synthetic Datasets

Synthetic object datasets have remained popular particularly among researchers in computer vision and graphics since the early 2000s. We have listed some of the popular datasets since 2003 until 2018 in the table below. We observed that both graphics and vision researchers have focussed either on the geometry (in the form of meshes and point clouds) or variation among the classes of shapes but very little about their use within physics engines for control. Therefore, until recently, most datasets did not provide any articulation information (hinges or joints) of the objects and their parts. 

> We refer to articulations as kinematic constraints in the form of hinges and joints. They are useful in animating a particular object in a physics engine.


|           Dataset          | Year |    Articulations   |                                Source Link                               |
|:--------------------------:|:----:|:------------------:|:------------------------------------------------------------------------:|
|   NTU 3D Model  Benchmark  | 2003 |         :x:        |                        http://3d.csie.ntu.edu.tw/                        |
|  Mesh Deformation Dataset  | 2004 |         :x:        |     http://people.csail.mit.edu/sumner/research/deftransfer/data.html    |
|         PrincetonSB        | 2004 |         :x:        |                 http://shape.cs.princeton.edu/benchmark/                 |
| AIM@SHAPE Shape Repository | 2006 |         :x:        |      http://visionair.ge.imati.cnr.it/ontologies/shapes/releases.jsp     |
|  McGill 3D Shape Benchmark | 2008 |         :x:        |                http://www.cim.mcgill.ca/~shape/benchMark/                |
|          SHREC' 08         | 2008 |         :x:        |              https://engineering.purdue.edu/PRECISE/shrec08              |
|   Columbia Grasp Database  | 2009 |         :x:        |                     http://grasping.cs.columbia.edu/                     |
|          SHREC' 10         | 2010 |         :x:        |       http://tosca.cs.technion.ac.il/book/shrec_robustness2010.html      |
|  Toyohashi Shape Benchmark | 2012 |         :x:        |                http://www.kde.cs.tut.ac.jp/benchmark/tsb/                |
|            3DNet           | 2012 |         :x:        |                		3d-net.org                		    |
|            IKEA            | 2013 |         :x:        |                        http://ikea.csail.mit.edu/                        |
|          PASCAL3D+         | 2014 |         :x:        |              http://cvgl.stanford.edu/projects/pascal3d.html             |
|            CAPOD           | 2014 |         :x:        |           https://sites.google.com/site/pgpapadakis/home/CAPOD           |
|          ModelNet          | 2015 |         :x:        |                     http://modelnet.cs.princeton.edu/                    |
|            NIST            | 2016 | :heavy_check_mark: | https://catalog.data.gov/dataset/nist-cad-models-and-step-files-with-pmi |
|          Thingi10K         | 2016 |         :x:        |                 https://ten-thousand-models.appspot.com/                 |
|         ObjectNet3D        | 2016 |         :x:        |              http://cvgl.stanford.edu/projects/objectnet3d/              |
|          ShapeNet          | 2016 |         :x:        |                         https://www.shapenet.org/                        |
|           PartNet          | 2018 | :heavy_check_mark: |                 https://cs.stanford.edu/~kaichun/partnet/                |
|             ABC            | 2018 |         -          |                   https://arxiv.org/pdf/1812.06216.pdf                   |

Note that some of the links in the table may be outdated now but we added them anyway as this is where the datasets were uploaded first.

![](/assets/img/2019-01-15/time_line.jpg)

Moreover, we have observed that the size of publicly available datasets of synthetic 3D objects has continued to grow linearly on logarithmic scale *i.e.* the size of the biggest dataset has increased by a factor of ~10 with particular interest from the researchers working on deep learning allowing the algorithms to scale to that enormity of data. We also observe that most of the researchers have focussed on a particular set of 3D objects *e.g.* chairs, tables and sofas.

<img src="/assets/img/2019-01-15/object_datasets.jpg" width="640" style="border: 0pt none; float:left; padding-right:10px; padding-bottom:10px">

<p>It is worth emphasising that</p>

- Although ShapeNet contains 3M models, only ~57K models have been cleaned and released publicly. Hence a lighter colour on the ShapeNet bar in the graph.
- PartNet builds on top of ShapeNet and adds hierarchical part based annotations and provides object articulation information that could be useful in virtual environments for robot learning. 
- ObjectNet3D uses a large fraction of models from ShapeNet in addition to the ones mined from the 3DWarehouse.
- The ABC dataset is not publicly available yet (at the time of writing this post). The majority of the models are mechanical parts and not typical categories of objects like chairs, tables *etc*.

<br>
We would also like to mention the popular [Dex-Net 1.0](https://github.com/BerkeleyAutomation/dex-net/raw/gh-pages/docs/dexnet_icra2016_final.pdf) dataset which is composed of 13,252 3D mesh models collected from assorted mix of various synthetic as well as real world datasets: 8,987 from the SHREC 2014 challenge dataset, 2,539 from ModelNet40, 1,371 from 3DNet, 129 from the KIT object database, 120 from BigBIRD and 80 from the YCB dataset.

<!--<details><summary>CLICK ME</summary><p>

#### yes, even hidden code blocks!

```
function test() {
  console.log("notice the blank line before this function?");
}
```
</p>
</details>-->


Importantly, we note that most datasets tend to have huge class imbalance among various categories. The image below shows the breakdown of ShapeNetCore (part of ShapeNet) that has ~57K models --- the biggest publicly released 3D model dataset as of yet. As we can see, it has large number of models for categories like chairs, tables, sofas, cabinets but relatively few for bed, bowl, can.

![](/assets/img/2019-01-15/ShapeNetCore.jpg)

Overall, datasets like ModelNet and ShapeNet have been extremely valuable in computer vision and robotics. For instance, ModelNet10 has been used in [VoxNet](https://www.ri.cmu.edu/pub_files/2015/9/voxnet_maturana_scherer_iros15.pdf) and [OctNet](http://openaccess.thecvf.com/content_cvpr_2017/papers/Riegler_OctNet_Learning_Deep_CVPR_2017_paper.pdf), ModelNet40 for 3D object detection from raw point cloud in [PointNet](https://arxiv.org/pdf/1612.00593.pdf) and [PointNet++](https://arxiv.org/pdf/1706.02413.pdf) while ShapeNet has been particularly useful in benchmarking robotic grasping. The popular [DexNet](https://berkeleyautomation.github.io/dex-net/) has evolved over the years benchmarking grasping using models from ShapeNet. The work of [Bousmalis et al.](https://arxiv.org/abs/1709.07857), [Tobin et al.](https://arxiv.org/abs/1710.06425) and recently [James et al.](https://arxiv.org/pdf/1812.07252) have all trained large scale models on grasping using freely available ShapeNet models.


#### Challenges of curating a synthetic dataset
Curating a large scale synthetic dataset can be extremely labourious endeavour. Even if the objects are publicly available there are still a lot of challenges involved

- Publicly available 3D models tend to require lot of manual filtering *e.g.* some 3D models have duplicate vertices and normals that violate the CCW (Counter Clock Wise) assumptions, duplicate and sometimes contradicting normals for the same face or broken 3D models to name a few. [Mitsuba-ShapeNet](https://github.com/shi-jian/mitsuba-shapenet) and [SceneNet RGB-D](https://robotvault.bitbucket.io/scenenet-rgbd.html) have written custom rendering shaders to bypass the rendering issues that come with 3D models with duplicate vertices and normals. Additionally, some 3D models come with two separate meshes and require stitching.
- Some 3D models have missing textures or lack material information. For instance, some objects have the path of material information set to the path on the local computer of the designer and this sometimes results in missing texture information. Additionally, the [UV-mapping](https://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics) of the vertices tends to be wrong at times resulting in unexpected wrapping of texture on the mesh.
- Most beginners working on websites that offer cloud services to create 3D models tend to leave their basic or unfinished models in the online shared repositories. Therefore, unless you download and go through the models it is hard to filter them out.
- Various hobbyists and beginners also create 3D models that do not come with metric information. This requires scaling them back to metric units so they are physically meaningful.
- It is also important to have all the models registered in a canonical reference frame so they can be arbitrarily rotated if needed for any future purposes. However, this is not always the case.
- If these models are to be used in physics engines or bounding box collisions detection, they require collision shapes (generally a convex hull or convex decomposition of the mesh). Therefore, they require additional processing with external softwares like [V-HACD](https://github.com/kmammou/v-hacd) to decompose the mesh into piecewise convex meshes.
- Meshes that have dense point clouds require skeletonisation as rendering time increases proportionally with the number of 3D points.
 
More dataset info here https://github.com/timzhang642/3D-Machine-Learning


### Real World Datasets

|        Dataset       | Year |    Articulations   |                          Source Link                          |
|:--------------------:|:----:|:------------------:|:-------------------------------------------------------------:|
|         B3DO         | 2011 |         :x:        |                     http://kinectdata.com/                    |
| RGB-D Object Dataset | 2011 |         :x:        |        http://rgbd-dataset.cs.washington.edu/index.html       |
|          KIT         | 2012 |         :x:        | https://journals.sagepub.com/doi/abs/10.1177/0278364912445831 |
|        BigBird       | 2014 |         :x:        |                http://rll.berkeley.edu/bigbird/               |
|          YCB         | 2015 |         :x:        |                 http://www.ycbbenchmarks.com/                 |
|        3DScan        | 2016 |         :x:        |                http://redwood-data.org/3dscan/                |
|        T-LESS        | 2017 |         :x:        |                http://cmp.felk.cvut.cz/t-less/                |
|          RBO         | 2018 | :heavy_check_mark: |         https://tu-rbo.github.io/articulated-objects/         |


![](/assets/img/2019-01-15/time_line_real.jpg)

> For physics simulation, articulations in the form of hinges and joints as well as collisions shapes of objects in the form of bounding volumes etc. are important.

<center><img src="/assets/img/2019-01-15/book_cabinet_rubiks.gif" height="200"></center>

#### Challenges of curating real world dataset

- Collecting large scale real world data is extremely labour intensive. There have been attempts in the past like [Kinect@Home](https://twitter.com/KinectatHome) to collect data via crowdsourcing but have been unsuccessful unfortunately.
- Scanning water-tight models can be extremely tricky if the model has kinematic joints and dynamics involved with them, or the object is resting against another where reaching a certain part of the object is not possible without moving the object. This process is extremely hard to automate.
- Most of the scanning requires setting up multiple cameras or a person going around the object to obtain multiple views and registering them in one refererence frame, camera calibration and constrained set-up where the object is placed. Any slight changes to the set-up may require calibration without which the registration errors quickly compound.


More datasets in the table here https://arxiv.org/pdf/1502.03143.pdf


### What should an ideal object dataset look like then? 

- Should contain large variety of objects and intra-class variability. The dataset should also aim to have uniform distribution of all kinds of classes to avoid any bias towards a particular set.
- Preferably synthetic as collecting water-tight models of real world objects still remains very challenging. Not because it requires labourious scanning of the object from multiple views but it requires the intent of the reconstruction to be conveyed to the robot or user. This is more relevant when scanning objects that have hinges and joints *e.g.* one needs to open the cabinet (the intent here is to open) to see what is inside and how to scan it and ensure that the scans are registered appropriately with the previously collected ones. Scanning what is behind the object is also difficult. Therefore, synthetic object models will likely be essential to sidestep these problems. 
- Preferably CAD models so they can be sampled at arbitrary resolution without any loss of data. They are metrically accurate and can be converted to STL or OBJ format (vice-versa is lossy). Additionally, if you are stitching different CAD models together the relative rotation and translation can be easily obtained via a CAD software. This avoids the calibration/registration process that one has to do on the real world data. Furthermore, they can be 3D printed and therefore provide a perfect simulation to real world match of the 3D model.
- Should come with various object intrinsic properties like [collision shapes](https://www.toptal.com/game/video-game-physics-part-ii-collision-detection-for-solid-objects), physical properties (*e.g.* friction, center of mass, inertia) as well as articulation information so they can be used directly into a physics engine. If properties like friction, mass, inertia etc. are not provided there are certainly ways to estimate them via [analysis-by-synthesis approaches](https://www.robots.ox.ac.uk/~vgg/rg/slides/galileo_slides.pdf) or calibrating the simulator to the real world with particle filters. However, it is also possible that this calibration process might yield parameters that are optimal given the objective function but not necessarily physically meaningful.

We note that despite the availability of these large scale datasets, artists and designers are needed to create bespoke 3D object models and assets --- a term often called content creation. This is time consuming and requires multiple iterations between the client and the designer. 

<!--Collision Shapes: https://www.toptal.com/game/video-game-physics-part-ii-collision-detection-for-solid-objects
STL format explanation https://all3dp.com/what-is-stl-file-format-extension-3d-printing/
OBJ format https://all3dp.com/1/obj-file-format-3d-printing-cad/-->



#### Authors 
Ankur Handa and Miles Brundage


#### Acknowledgements 
Arsha Nagrani, Avital Oliver, Fei Xia,

#### Credits
Credits: https://partsolutions.com/wp-content/uploads/2017/09/The-history-of-CAD_CADENAS_R3.png

ShapeNet doc http://shapenet.cs.stanford.edu/shapenet/obj-zip/ShapeNetCore.v2-old/shapenet/tex/2016Proposal/2016shapenet_main.pdf

ShapeNet breakdown http://shapenet.cs.stanford.edu/shapenet/obj-zip/ShapeNetCore.v2-old/shapenet/tex/TechnicalReport/main.pdf

<div align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/YB3saviItTI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
