# geohash-iOS

geohash-iOS is an implementation of GeoHash based spacial proximity calculation in Objective-C to be used for mobile applications. It contains the necessary classes and a tester to check the functionality.

## GeoHashes

A GeoHash is a representation for a certain location on the world map. It is encoded through an amount of base32 characters depending on a given precision. The string can be transfered into a binary representation where the even bits are extracted to calculate longitude and the odd bits to calculate latitude correspondingly.

GeoHashes are easy to handle compared to the numerical latitude/longitude values. In that way they are good for data processing and storage of point data.

A good detailled description can be found at [Wikipedia](http://en.wikipedia.org/wiki/Geohash). 

## Usage

The main-method is to be found in the supporting files folder in the file main.m. The test method is testGeoHashes in the GNViewController class.

### Calculate a GeoHash from a given numerical latitude/longitude representation of a point

```objective-c
float lat = 21.567;
float lon = -175.321;
int precision = 4;
GNGeoHash *gh = [GNGeoHash withCharacterPrecision:lat andLongitude:lon andNumberOfCharacters:precision];

//print the result
NSLog(@"GeoHash is %@",gh);

//get GeoHash
NSString *hashString = [gh toBase32];
```

### Calculate Neighbors

```objective-c
GNGeoHash *gh = [GNGeoHash withCharacterPrecision:lat andLongitude:lon andNumberOfCharacters:precision];

GNGeoHash *northern = [gh getNorthernNeighbour];
GNGeoHash *eastern = [gh getEasternNeighbour];
GNGeoHash *southern = [gh getSouthernNeighbour];
GNGeoHash *western = [gh getWesternNeighbour];

//print results
NSLog(@"Northern hash is %@",northern);
NSLog(@"Eastern hash is %@",eastern);
NSLog(@"Southern hash is %@",southern);
NSLog(@"Western hash is %@",western);
```

### Obtain numerical latitude/longitude values for the area described by the given GeoHash

### Obtain numerical latitude/longitude values for the area described by the given GeoHash

```objective-c
GNGeoHash *gh = [GNGeoHash withCharacterPrecision:lat andLongitude:lon andNumberOfCharacters:precision];

NSLog(@"Upper left corner is %@",[gh.boundingBox getUpperLeft]);
NSLog(@"Lower right corner is %@",[gh.boundingBox getLowerRight]);
```
### Check proximity to a certain location?

## Restrictions

* Latitude values have to be between -90 and 90
* Longitude values have to be between -180 and 180
* Precision has to be between 1 and 12

## Requirements
* iOS 5.1?

## License
*(This project is released under the [GPL](http://www.gnu.org/copyleft/gpl.html)*

Copyright (c) 2012 GNS Science. All rights reserved. http://www.gns.cri.nz/
