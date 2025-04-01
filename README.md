# leetmapping





# Geospatial Practice Questions


 - How to measure the distance from New York City, NY to London, UK, given their lattitude and longitude?
   - How about measuring the distance between two points in New York City?
  
 - Explain how WMS, WMTS, and XYZ Tiles work

 - Given a coordinate in latitude and longitude and its CRS (coordinate reference system), how can you reproject the coordinates to a new CRS?

 - What is the difference between vector data sets and raster data sets?

- Describe the differences between spatial indexes and spatial joins. What about spatial overlays?

## What is the State Plane Coordinate System (SPCS)?

#### Reading
[NOAA Special Publication NOS NGS 13](https://geodesy.noaa.gov/library/pdfs/SP_NOS_NGS_13.pdf "The State Plane Coordinate System - 2018")

### Notes

- A set of **124 geographic zones over the US**. The system is highly accurate within **each zone with an error of less than 1:10,000**, meaning the difference between a length of 10,000 meters on the ellipsoid and its representation on the map would be about 1 meter. It is roughly four times more accurate than **UTM**.
- **SPCS 2022** has up to **three zone layers in each state**, and the number of zones will vary greatly between states. Every U.S. state and territory will have a statewide zone. Most states will also have a multiple-zone layer that covers the entire state, and some states will also have a multiple-zone layer that covers only part of the state. In addition, there will be three “special use” zones that each cover more than one state.
  - The reason for large variation in the number of layers and zones is that stakeholders in many states actively participated in the SPCS 2022 design process. **41 states submitted 67 requests** and/or proposal forms for SPCS 2022 zones. Requests were for zones designed by NGS, and proposals were for zones designed by stakeholders. Proposals were reviewed and approved by NGS, **resulting in 28 states designing their own zones**.
- **SPCS 83** was created by the National Geodectic Survey in 1983; SPCS 83 consists of 125 zones based on the Lambert Conformal Conic, Transverse Mercator, and Oblique Mercator projections.
- In the 1930s, SPCS provided a way to perform "geodectic" survey using plane trigonometry, making it among the earliest practical means to access the National Spatial Reference System (NSRS)
- As early as 1817, in New York Harbor there was a **Survey of the Coast** as its first field project. In 1832, work spread and expanded along to the Gulf Coast and parts of the West Coast by 1851.
- In 1871, the **Transcontinental Arc of Triangulation** was undertaken to conduct a precise survey across the country.
- In 1930, the survey network spanned the entire country and formed a "lattice" pattern. Great Depression relief programs made great progress in expanding the survey network and now there is more than 1,500,000 positioned points in the NGS's database.

 **Mapping Concepts and Standards:**
  - [x] _Polyconic Projection_ by Ferdinand Hassler, the first superintendent of the Survey of the Coast, 1987
  - [x] _World Polyconic Grid_ by Army Map Service
  - [x] _Conformal Map Projections_ , two conformal projections were adopted around 1920, the Lambert Conformal Conic and the Gauss-Krüger form of the Transverse Mercator

  - Conformality enforces the condition that, at a point, angles are preserved and scale error is the same in all directions. These qualities preserve shape locally, and it makes them particularly useful for calculations involving directions, azimuths, and distances.
  - Both adopted properties of conformality and equal area preservation (which are mutually exclusive) are derived from Lambert's Composition of Terrestial and Celestial Maps

