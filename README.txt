          Replication   in MongoDB
Start the MongoDB server by specifying -- replSet option.
mongod --replSet priya --logpath "1.log" --dbpath "H:\rs0" --port 27017
mongod --replSet priya --logpath "2.log" --dbpath "H:\rs1" --port 27018
mongod --replSet priya --logpath "3.log" --dbpath "H:\rs2" --port 27019

create the configuration of replica sets
 config  = { _id:"priya", members:[{ _id: 0, host:"localhost:27017"},{_id:1,host:"localhost:27018"},{_id:2,host:"localhost:27019"}]};
{
        "_id" : "priya",
        "members" : [
                {
                        "_id" : 0,
                        "host" : "localhost:27017"
                },
                {
                        "_id" : 1,
                        "host" : "localhost:27018"
                },
                {
                        "_id" : 2,
                        "host" : "localhost:27019"
                }
        ]
}
In Mongo client, issue the command rs.initiate() to initiate a new replica set.
rs.initiate(conf)

To check the status of replica set issue the command 
rs.status()

now in primary node make the changes or write new data into the database 
use exampleDB
for (var i = 0; i <= 10; i++) db.exampleCollection.insert( { x : i } )

If your replica set is configured properly, the data should be present on your secondary members as well as the primary. To test this, connect to the mongo shell with the administrative user on one of your secondary members, and run the command
db.getMongo().setSlaveOk()

kill the primary node.Afte that when you connect to the secondary node it acts like primary and the data we have inserted through primary will be available in secondary node.
