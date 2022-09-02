[![license](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by.svg)](https://creativecommons.org/licenses/by/4.0/){target=_blank} 

# :material-cloud-braces: Introduction to Cloud Native & Analysis Ready Data Formats

#### Instructors(s): 

[Tyson Lee Swetnam PhD](https://tysonswetnam.com/){target=_blank} [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](http://orcid.org/0000-0002-6639-7181){target=_blank},
[Carlos Lizárraga-Celaya PhD](https://github.com/carloslizarragac){target=_blank} [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](https://orcid.org/0000-0002-0893-4268){target=_blank}

## About

This website follows the [FAIR](https://www.go-fair.org/fair-principles/){target=_blank} and [CARE](https://www.gida-global.org/care){target=_blank} data principles and hopes to help further open science. 

## Agenda

| Lessons | Estimated Time to Complete | Link |
|---------|----------------------------|------|
| Introduction to Cloud Native Data Types | 15 minutes | [presentation](https://docs.google.com/presentation/d/1MXOqsIC5TzPB8GH-UweZp3BxGMFrj-qPdPCHSOlqbjU/edit?usp=sharing){target=_blank} |
| [Hands on with GeoJSON](geojson.md) | 30 minutes | [GeoJSON.io](https://geojson.io){target=_blank} |
| [Hands on with Cloud Optimized GeoTIFF](cog.md) | 30 minutes | [cogeo.org](https://cogeo.org){target=_blank} |
| Break | 10 minutes | |
| [Hands on with XArray & Zarr](xarray.md) | 30 minutes | [Xarray](https://docs.xarray.dev/en/stable/){target=_blank}, [Zarr](https://zarr.readthedocs.io/en/stable/){target=_blank} |
| [Hands on with Cloud Optimized Point Clouds](copc.md) | 30 minutes | [COPC](https://copc.io/){target=_blank} |
| [Hands on with Spatio-Temporal Asset Catalogs](stac.md) | 30 minutes | [STAC](https://stacspec.org/){target=_blank} | 
| Summary and Conclusion | 5 minutes | | 

## Pre-requisites

* a laptop with an active wifi connection

### helpful but not required

* a basic understanding of the [Command Line Interface (UNIX)](https://swcarpentry.github.io/shell-novice/){target=_blank}
* a basic understanding of [Python3](https://www.geeksforgeeks.org/introduction-to-python3/#:~:text=Python%20is%20a%20high%2Dlevel,them%20readable%20all%20the%20time.){target=_blank}


## Why "cloud native"?

:material-cog: :material-layers-triple:   :material-vector-polyline:   :material-compass-rose:   :material-math-compass:   :material-map-clock: :material-map-marker:   :material-satellite-variant:   :material-airplane:   :material-drone:   :material-quadcopter:   :material-database-cog:   :material-graph-outline: 

There is a shift happening in the way we use Earth Observation System data to do research and management. Cloud data storage technologies have advanced at such a pace that we can now find and explore massive amounts of data via our web browser. At the same time online platforms with specialized software and hardware offer general data science and machine learning tools to explore these online datasets.

With these advances it is easier to foster collaborations, promote data-driven discovery, drive scientific innovation, increase transparency and improve reproducibility.

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/conventional.png" target="blank" rel="conventional">![conventional](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/conventional.png){ width="700" } </a>
    <figcaption> The old ways of receiving and working with GIS data. </figcaption>
</figure>

Many of us have been participants in "sneaker net" and "mail order" data delivery ordering and managing data transfers over physical media. These data are then processed on our workstations and laptop computers and ultimately put on external hard drives or uploaded back to national data services. GIS data have changed hands for years over conventional internet protocols (`https://`, `ftp://`, and newer `s3://`), where datasets are preferentially DOWNLOADED to our local compute resources and worked on.

"Cloud Native" means you are no longer looking to download all of your GIS data. Instead, we send our "code" and our execution tasks to the "Cloud" where the data are processed, and serviced over a variety of commercial cloud providers who are already hosting these large geospatial datasets (often free of cost to us).  Results can be viewed in the browser, or streamed in reduced formats back to our local computers.

<figure markdown>
  <a href="https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/cloud.png" target="blank" rel="cloud">![cloud](https://github.com/tyson-swetnam/agic-2022/raw/main/assets/images/cloud.png){ width="700" } </a>
    <figcaption> The Cloudy way </figcaption>
</figure>

Cloud-native and "Analysis Ready Data" formats allow us to work with large datasets on the cloud easily and rather painlessly.

<center>
<a href="https://geojson.io" style="float:left" target="blank" rel="geojson">![geojson](https://brands.home-assistant.io/_/geo_json_events/logo.png){ width="200" height="25" } </a>
<a href="https://stacspec.org" style="float:center" target="blank" rel="stac">![stac](https://d33wubrfki0l68.cloudfront.net/22691a3c3002324451ed99f4009de8aab761e1b7/d24da/public/images-original/stac-01.png){ width="200" height="25" } </a>
<a href="https://cogeo.org" style="float:right" target="blank" rel="cog">![cog](https://www.cogeo.org/images/logo/Cog-02.png){ width="200" height="50" } </a> 
</center> 

<center>
<a href="https://zarr.readthedocs.io" style="float:left" target="blank" rel="zarr">![zarr](https://zarr.readthedocs.io/en/stable/_static/logo1.png){ width="100" } </a>
<a href="https://docs.xarray.dev" style="float:center" target="blank" rel="xarray">![xarray](https://docs.xarray.dev/en/stable/_static/dataset-diagram-logo.png){ width="200" } </a> 
<a href="https://copc.io" style="float:right" target="blank" rel="copc">![copc](https://copc.io/COPC_IO-Logo-2color.png){ width="200" } </a> 
</center>

## Open Architectures

The new approach to data sharing, focused on object storage rather than file downloads. This cloud platform approach is scalable and instead of moving data to processing systems near users as is the tradition, brings processing, computing, analytics and visualization to data – so called data proximate workbench capabilities, sometimes also referred to as server-side processing.

<img src="https://miro.medium.com/max/1400/1*FkR2h8f_Lut00Uo_Pxogvg.png" width=480>

(Open Architecture for scalable cloud-based data analytics. From Abernathey, Ryan (2020): Data Access Modes in Science.)

---

## Light reading

Gentemann, C. L., et al. (2021). “Science Storms the Cloud”. AGU Advances, 2, e2020AV000354. https://doi.org/10.1029/2020AV000354

Abernathey, R. P.  et al. (2021) "Cloud-Native Repositories for Big Scientific Data," in Computing in Science & Engineering, vol. 23, no. 2, pp. 26-35, 1 March-April 2021, https://doi.org/10.1109/MCSE.2021.3059437
