---
layout: page
title: ACE-GCN
description: Adsorbate Chemical Environment-based Graph Convolutional Network
img: /assets/img/ace-gcn/ace_gcn.png
importance: 1
category: phd
---

There are plethora of reactions wherein the material (catalyst) aiding the reaction undergoes phhysical and/or chemical transformation under the reaction conditions (_in-operando_). Heterogeneous catalytic reactions are sensitive to atomic-scale complexities arising under in-operando conditions, such as variations in surface morphology, composition, and adsorbate-adsorbate interactions. More so, presence of irregular geometries and complex material arrangement, present for the catalyst, expands the possible solution space of possible catalyst models for the reaction. As a result, the difficulty in systematically generating and analyzing the surface representations, make atomic-model development non-trivial. To address this challenge, a graph network-based enumeration and prediction strategy is explored. 

Adsorbate Chemical-Environment-based Graph Convolution Neural Network (ACE-GCN), is a versatile framework with the ability to encode atomic configurations comprising of diverse adsorbates, binding locations, coordination environments, and variations in the substrate morphology. This workflow is used to generate and rank surface adsorbate configurations for reactions which are shown to be affected by the presence of high adsorbate surface coverage. Through this study we inch closer towards realizing the deam of better describing the molecular-level functioning for complex materials and process. 

## Background

Encoding catalyst surfaces for machine learning-based screening is a fairly recent expansion of the machine learning (ML) methods in computational material modeling. Exciting advances in database architecture, feature abstractions, and compute power have now made it possible to consider avenues of encoding complex information. Thanks to these advances, researchers are now considering catalysts models that are much wider in composition space, and modeling complex reaction networks that were hitherto deemed challenging. In most of these model development endevors the challenges are: (1) Feature representation of the atomic models which are machine readable and (2) Systematically generating the training dataset with minimal bias from the user to ensure exhaustive sampling of the search space. 

One way of addressing this challenge is to use graph-networks for presenting the atoms and their bonding environment. This idea has been implemented in understanding social interactions, relationship between entities as seen in [Indian spice usage](https://pgg1610.github.io/blog_fastpages/python/exploratory-data-analysis/data-visualization/web-scrapping/2020/12/09/food_relations.html), and in modeling, predicting molecular properties of small molecules which intuitively are condusive to such graphical network representation.

<img class="img-fluid rounded z-depth-1" src="{{ site.baseurl }}/assets/img/ace-gcn/graphs.png" width="1000" data-zoomable>

<div class="caption">
Leveraging the expressing power of graph networks to describe relational datasets 
</div>

In this work we build upon the idea of graph network representation and use sub-graphs to represent high coverage coverage representations. Every sub-graph is generated using the chemical environment of each unique adsorbate in the system. 

***

## ACE-GCN 

Adsorbate Chemical Environment-based Graph Convolutional Neural Network (ACE-GCN, for short) is a framework to help systematically generate, encode, and predict energetics of the surface models to help navigate the phase space to find stable surface representations. 

<img class="img-fluid rounded z-depth-1" src="{{ site.baseurl }}/assets/img/ace-gcn/workflow.png" width="1000" data-zoomable>

<div class="caption">
<b>ACE-GCN algorithm to encode and train high coverage adsorbate configurations.</b> (1) Generate sub-graphs: each configuration is split into multiple subgraphs, as identified by the [SurfGraph](https://surfgraph.readthedocs.io/en/latest/) algorithm. A distinct ego-graph is generated for each adsorbate to encode local geometric and chemical properties around the adsorbate in a subgraph representation. (2) Subgraph Featurization: each atom and its corresponding bond attribute in the subgraph is expressed as a vector representation according to the chemical identity (elemental properties) and spatial bond distance, termed as node and edge features, respectively. (3) Subgraph Convolutions: every node vector in the subgraph is iteratively updated through multiple rounds of graph convolution operations, which account for the atom’s geometric and chemical neighborhood using node and edge vectors of the neighboring atoms. (4) Fingerprints: a hierarchical pooling operation condenses all subgraphs for every adsorbate into one fingerprint vector. (5) NN Layer: the fingerprint vector is passed to a feed-forward neural network (NN) which maps it to the target property of choice, such as the average adsorption energy.
</div>

ACE-GCN leverages the expressive power of graph networks to encode and learn the mapping of electronic and geometrics features of the catalyst surface to its thermodynamic stability. Once trained, the model can be used to rank new surface representations and quickly select stable candidates. 

The atomic-scale catalyst models and computation tools proposed through this work can serve as a starting point for developing a detailed description of complex catalyst surfaces under in-operando conditions, ultimately leading to fundamental insights into the factors that govern the functioning of heterogeneous catalysis in chemically complex environments.

***

## Application to heterogeneous catalysis

We utilize this workflow to successfully sample the large number of atomic configurations to identify the most relevant surface representation stable reaction conditions. We demonstrate the utility of the workflow to determine the relevant high coverage configurations for the cases of adsorbed NO* on Pt<sub>3</sub>Sn (111) surface and that of adsorbed OH* on irregular Pt (221). 

The first case presents complexities because of the presence of an alloy and the strong binding nature of NO, while the second case presents challenges arising from the presence of step defects and the ability of OH to form inter-molecular hydrogen bonds. Using these two test cases as representative examples for likely challenges when developing computational models, we demonstrate the generalizability of our workflow to identify the most relevant atomistic configurations by utilizing only 10% of the total possible configurations. 


<img class="img-fluid rounded z-depth-1" src="{{ site.baseurl }}/assets/img/ace-gcn/feedback_loop.png" width="1000" data-zoomable>

<div class="caption">
Proposed workflow to address increasing complexity in heterogeneous catalyst model development when decribing in-operado representation.  
</div>

This approach can serve as a starting point for developing detailed atomic description of complex catalyst surfaces under _in-operando_ conditions, ultimately leading to fundamental insights into factors that govern heterogeneous catalysis in structurally and chemically complex environments.

***

### Future Reading:

Xie, T. & Grossman, J. C. Crystal Graph Convolutional Neural Networks for an Accurate and Interpretable Prediction of Material Properties. Phys. Rev. Lett. 120, 145301 (2018). [Blog](http://txie.me/blogs/cgcnn-3d/)

Goodall, R.E.A., Lee, A.A. Predicting materials properties without crystal structure: deep representation learning from stoichiometry. Nat Commun 11, 6280 (2020). 

Back, S. *et al.* Convolutional Neural Network of Atomic Surface Structures to Predict Binding Energies for High-Throughput Screening of Catalysts. *J. Phys. Chem. Lett.* **10**, 4401–4408 (2019) 

Lym, J., Gu, G. H., Jung, Y. & Vlachos, D. G. Lattice convolutional neural network modeling of adsorbate coverage effects. *J. Phys. Chem. C* **123**, 18951–18959 (2019).

Schmidt, D. J.; Chen, W.; Wolverton, C.; Schneider, W. F. Performance of Cluster Expansions of Coverage-Dependent Adsorption of Atomic Oxygen on Pt(111). J. Chem. Theory Comput. 2012, 8, 264−273

Chowdhury, A. J. *et al.* Prediction of Adsorption Energies for Chemical Species on Metal Catalyst Surfaces Using Machine Learning. *J. Phys. Chem. C* **122**, 28142–28150 (2018).


<!--
Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/1.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/3.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/5.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/5.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.

Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal it's glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/6.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/11.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/" target="_blank">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/6.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/11.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
```
-->
