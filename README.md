## loopback-connector-mongodb (internally modified package)

This is a modified version of the MongoDB connector for LoopBack. 
### Changes from original version:
 * Mapping LoopBack's GeoPoint to MongoDB's GeoJSON: this change was based on https://github.com/timosaikkonen/loopback-connector-mongodb
    Model can include locations as GeoPoints, while they will be stored in MongoDB as GeoJSON objects, allowing for geo-special indexing and queries.
 * Supporting transparent use of MongoDB's $near queries as parameters for find function calls from LoopBack: 

    find({ where:{
                    location: { $near : { $geometry: { type: "Point",  coordinates: [-122.540408, 38.061837] }, $maxDistance: 5000 } }
            }
        }, cb );

From original readme:

MongoDB connector for loopback-datasource-juggler.

Please see the full documentation at [docs.strongloop.com](http://docs.strongloop.com/display/LB/MongoDB+connector).

## Customizing MongoDB configuration for tests/examples

By default, examples and tests from this module assume there is a MongoDB server
instance running on localhost at port 27017.

To customize the settings, you can drop in a `.loopbackrc` file to the root directory
of the project or the home folder.

**Note**: Tests and examples in this project configure the data source using the deprecated '.loopbackrc' file method, 
which is not suppored in general.
For information on configuring the connector in a LoopBack application, please refer to [LoopBack documentation](http://docs.strongloop.com/display/LB/MongoDB+connector).

The .loopbackrc file is in JSON format, for example:

    {
        "dev": {
            "mongodb": {
                "host": "127.0.0.1",
                "database": "test",
                "username": "youruser",
                "password": "yourpass",
                "port": 27017
            }
        },
        "test": {
            "mongodb": {
                "host": "127.0.0.1",
                "database": "test",
                "username": "youruser",
                "password": "yourpass",
                "port": 27017
            }
        }
    }

**Note**: username/password is only required if the MongoDB server has
authentication enabled.

## Running tests

    npm test

## Release notes

  * 1.1.7 - Do not return MongoDB-specific _id to client API, except if specifically specified in the model definition
