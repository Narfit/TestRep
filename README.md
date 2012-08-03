# geohash-iOS

geohash-iOS is an implementation of GeoHash based spacial proximity calculation in Objective-C to be used for mobile applications. It contains the necessary classes and a tester to check the functionality.

## GeoHashes

A GeoHash is a representation for a certain location on the world map. It is encoded through an amount of base32 characters depending on a given precision. The string can be transfered into a binary representation where the even bits are extracted to calculate longitude and the odd bits to calculate latitude correspondingly.

GeoHashes are easy to handle compared to the numerical latitude/longitude values. In that way they are good for data processing and storage of point data.

To check the position of a hash, go to [geohash.org](geohash.org). Add the hash string to the URL (e.g. for hash r3gqm68z9gnw enter [geohash.org/r3gqm68z9gnw](geohash.org/r3gqm68z9gnw) as URL.

A good detailled description can be found at [Wikipedia](http://en.wikipedia.org/wiki/Geohash). 

## Usage

The main-method is to be found in the supporting files folder in the file main.m. The test method is testGeoHashes in the GNViewController class.

### Calculate a GeoHash from a given numerical latitude/longitude representation of a point

```objective-c
float lat = -34.042580;
float lon = 151.052139;
int precision = 12;

GNGeoHash *gh = [GNGeoHash withCharacterPrecision:lat andLongitude:lon andNumberOfCharacters:precision];

//print the result
NSLog(@"GeoHash is %@",[gh toBase32]);
```

Result is
```
GeoHash is r3gqm68z9gnw
```

### Calculate Neighbors

```objective-c
GNGeoHash *gh = [GNGeoHash withCharacterPrecision:lat andLongitude:lon andNumberOfCharacters:precision];

GNGeoHash *northern = [gh getNorthernNeighbour];
GNGeoHash *eastern = [gh getEasternNeighbour];
GNGeoHash *southern = [gh getSouthernNeighbour];
GNGeoHash *western = [gh getWesternNeighbour];

//print results
NSLog(@"Northern hash is %@",[northern toBase32]);
NSLog(@"Eastern hash is %@",[eastern toBase32]);
NSLog(@"Southern hash is %@",[southern toBase32]);
NSLog(@"Western hash is %@",[western toBase32]);
```

Result is
```
Northern hash is r3gqm68z9gnx
Eastern hash is  r3gqm68z9gny
Southern hash is r3gqm68z9gnt
Western hash is W has GeoHash r3gqm68z9gnq
```

### Obtain numerical latitude/longitude values for the area described by the given GeoHash

```objective-c
GNGeoHash *gh = [GNGeoHash withCharacterPrecision:lat andLongitude:lon andNumberOfCharacters:precision];

NSLog(@"Upper left corner is %@",[gh.boundingBox getUpperLeft]);
NSLog(@"Lower right corner is %@",[gh.boundingBox getLowerRight]);
```

Result is
```
Upper left corner is (-34.042580,151.052139)
Lower right corner is (-34.042580,151.052140)
```
## Restrictions

* Latitude values have to be between -90 and 90
* Longitude values have to be between -180 and 180
* Precision has to be between 1 and 12

## Requirements
* iOS 5.1

## License
*(This project is released under the [GPL](http://www.gnu.org/copyleft/gpl.html))*

Copyright (c) 2012 GNS Science. All rights reserved. http://www.gns.cri.nz/
