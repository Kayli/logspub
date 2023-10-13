# notes related to geodesy

## basics

- geodesy: is the scientific discipline that focuses on measuring and understanding the Earth's shape, size, and gravitational field, as well as the variations in these parameters over time

- geodetic line (geodesic line, great circle)
  - is the shortest path between two points on the surface of a sphere, such as the earth
  - it follows the natural curvature of the sphere
  - is typically considered to be infinite in length
  - geodetic lines are continuous and extend without end
  - 'geodetic' spelling is used for adjective, 'geodesic' spelling used for noun

- geodetic segment
  - is a portion or segment of a geodetic line
  - it connects two specific points on the surface of the earth or a spherical object
  - it is a finite part of a geodetic line
  - typically used for practical purposes
    - such as calculating distances and directions between two defined locations
  - have distinct starting and ending points

- wgs84: world geodetic system of 1984
  - is a standard used in cartography, geodesy, and satellite navigation including GPS
  - defines an Earth-centered, Earth-fixed coordinate system and a geodetic datum
  - also describes the associated Earth Gravitational Model and World Magnetic Model

- geodetic datum
  - is a reference framework used to specify the location of geographic features on the Earth's surface

- grid north vs true north
  - grid north is used to navigate close to the north pole area
  - there are modern navigation systems which provide grid north direction

- height vs altitude
  - height is a distance from the ground
  - altitude is a distance from the mean sea level

- earth
  - ratio of elipticity: 1/298
  - period of rotation around sun: 365.25 days
    - anticlockwise when viewed from the north pole
      - around its axis as well as around the sun
  - equator plane is set off by 23.5 degrees relative to orbital plane
  - arctic is at the north pole, antarctic is at the south pole
  - perihelion: closest point to the sun
  - aphelion: farthest point from the sun
  - equinoxes
    - two midpoints in the orbit where day equals night


## kepler laws
  
- the orbit of each planet is an ellipse and the sun is at one focus
  - ellipse foci (there are 2): always lie on the major axis, and the sum of the distances from the foci to any point on the ellipse (the constant sum) is greater than the distance between the foci

- a line joining a planet and the sun sweeps equal areas during equal time periods


## grid system
  
- two sets of lines (latitude and longitude) that cross each other

- latitude
  - horizontal lines (geodesics)
    - which are circles of a cross section with planes parallel to the plane of equator
  - equator is 0 degrees, -90 degrees at south pole and 90 degrees at north
  - to increase precision 'minutes' and 'seconds' are used
  - 2 types
    - geocentric latitude
      - less precise
      - angle between equator plane and line that goes through center of the earth and point on surface 
      - does not consider spheroid shape of the earth
    - geographic latitude
      - more precise
      - angle between equator plane and normal of the plane tangent to the surface of the earth
  - 1 minute of latitude = 1 nautical mile = 1.85200 km

- longitude
  - vertical lines (geodesics) from north to south
  - prime meridian is at 0 degrees longitude
    - passing through greenwich observatory, london
  - distance: longitude * 60nm * cos(latitude)


## references

[1]: https://www.youtube.com/playlist?list=PLncfeagBRbBd8MTQd_jNSxKKXM6jzBkK7 (ATPL General Navigation course)