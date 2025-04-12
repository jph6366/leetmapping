# leetmapping





# Geospatial Practice Questions


 ## What is the most accurate method of measuring distance between two points on Earth?

### Reading
- [calculations for lati­tude/longi­tude points, with the formulas and code fragments for implementing them](https://www.movable-type.co.uk/scripts/latlong.html)
- [Vincenty solutions of geodesics on the ellipsoid](https://www.movable-type.co.uk/scripts/latlong-vincenty.html)
- [algorithms for the computation of geodesics on an ellipsoid of revolution are given](https://link.springer.com/article/10.1007/s00190-012-0578-z)
  - Charles Karney has improved on Vincenty’s method with a method which has errors in nanometers (and always converges on antipodal points)
- [GeographicLib is collection of libraries by Charles Karney which started in 2008.](https://geographiclib.sourceforge.io/)
  - The C++ library now offers:
    - geodesic and rhumb line calculations;
    - conversions between geographic, UTM, UPS, MGRS, geocentric, and local cartesian coordinates;
    - gravity (e.g., EGM2008) and geomagnetic field (e.g., WMM2020) calculations.


 #### The first question one must ask is what coordinate reference system (CRS) are these two points represented in
   - Assuming 2D Geographic coordinates (longitude, latitude)
 #### The followup question should then be how precise are our coordinates?
   - Meaning what degree to which is the longitude and lattitude pins down an actual point on Earth.
   - In Computer Science, a **64 bit floating point precision** is required to represent geodectic coordinates accurately. This includes both geocentric coordinates, which are typically very large numbers, and geographic coordinates, which are smaller but very precise numbers. Wherever possible use 64-bit floating point types for representing geodetic coordinates
     - In C++ use double instead of float, likewise use glm::dvec3 instead of glm::vec3.
     - In Unity use Unity.Mathematics.double3 instead of Vector3.
     - In JavaScript numbers are always stored as double precision floats. However, take care when using typed arrays to avoid Float32Array.
     - The blog post Precisions, Precisions goes over some strategies for rendering global scale coordinates on the GPU with high precision.
       
   - Approximately one degree of latitude covers

     10<sup>7</sup>/ 90 = 111,111 m

   - And a degree of longitude covers is about the same
  
   - Thus, it is always safe to figure that the

   **sixth decimal place in one decimal degree has 111,111 / 10<sup>6</sup> = about 1/9 meter = ~4 inches of precision**
   
   #### What about about other decimal places?
    
    - the first decimal place = ~11.1 km
    - the second decimal place = ~1.1 km
    - the third decimal place = ~110 m
    - the fourth decimal place = ~11 m
    - the fifth decimal place = ~1.1 m
    - the sixth decimal place = ~11 cm
    - the seventh decimal place = ~1.1 cm
    - the eighth decimal place = ~1.1 mm
    - the ninth decimal place = ~110 microns
   ...
   - Thirteen decimal places will pin down the location to...

   **111,111 / 10<sup>13</sup> = 1 angstrom ; around half the thickness of a small atom**

  #### What's the difference between geocentric and geodetic latitude?

  - I also forgot to mention the Earth is oblate spheroid rather than a sphere so there are two different systems for desecribing latitude
  - A point described using geocentric latitude and a point described using geodetic latitude can differ by tens of kilometers.

![image](https://github.com/user-attachments/assets/7e195e42-1857-49ce-88c1-5eb1c11c68be)
 
  - Only the **geodetic surface normal** should be used when precision matters

 #### Now one can infer the level of precision of our coordinates, so how does one go about measuring the distance between two points on Earth?

- Well if one were measuring on a sphere then the **Spherical Law of Cosines** or the **Haversine Formula**. Using these on an ellipsoid typically result in less than 0.3% errors.
  - Although the Law of Cosines is preferable to the Haversine Formula due to the formula [not entailing the evaluation of trigonometric functions](https://gis.stackexchange.com/questions/4906/why-is-law-of-cosines-more-preferable-than-haversine-when-calculating-distance-b?rq=1#:~:text=A%20historical%20footnote%3A).

  - pseudo-code for cosine formula
  
          distance = acos(SIN(lat1)*SIN(lat2)+COS(lat1)*COS(lat2)*COS(lon2-lon1))*6371
  
  - pseudo-code for haversine formula
  
          dLat = (lat2-lat1)
          dLon = (lon2-lon1)
          a = sin(dLat/2) * sin(dLat/2) + cos(lat1) * cos(lat2) * sin(dLon/2) * sin(dLon/2)
          distance = 6371 * 2 * atan2(sqrt(a), sqrt(1-a))    
    
- But if one is measuring on an oblate spheroid, then one can opt to use **Vincenty's Formula**
  - **Vincenty’s solution for the distance between points on an ellipsoidal earth model is accurate to within 0.5 mm distance,0.000015″ bearing,** on the ellipsoid being used.
  - Vincenty’s inverse solution can fail on nearly antipodal points, two points of a sphere are called antipodal or diametrically opposite if they are the endpoints of a diameter, a straight line segment between two points on a sphere and passing through its center. This can happen with distances greater than 19,936 km, or within around 75 km of the antipodal point.

  ![image](https://github.com/user-attachments/assets/754e9502-090a-4a78-a997-2d8103c55c5d)

- **Millimetre precision is stretching the limits of geodetic survey techniques**: very few points will have been surveyed to such precision
  - Further, the familiar WGS-84 (World Geodetic System 1984) has no ‘physical realisa­tion’ – it is not tied to geodetic groundsta­tions, just to satellites – and is defined to be accurate to no better than around ±1 metre
  - Working to an accuracy of better than ±1 metre, plate tectonic movements become significant. Depending on the datum it’s defined in, any given point will most likely have shifted many millimetres from where it was last year.
    - The [**International Terrestial Reference System and Frame**](https://itrf.ign.fr/en/homepage) was developed where the latitude/longitude of a coordinate of a position will vary over time.
  - So for millimetre accuracy to be relevant, you need to know a fair bit about the reference frames, datums, and epochs of your coordinates, and other param­eters of your measure­ments. 
![image](https://github.com/user-attachments/assets/80e662e7-bb13-4b9d-be25-ccd36fa5e269)


# miscellaneous
  
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

