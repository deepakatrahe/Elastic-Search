# Elastic-Search


CRUD operation in Elastic Search Using Kibana
In this article lets discuss about the how we can do CRUD operation in Elastic Search using Kibana.

We will be dealing with how to manage data.

In elastic the HTTP verb is used as a way to specify which action we would like to perform on some resource, in this case an index.

In elastic tables are known as an indices, columns known as mappings.

We can add an index named “employee” using “PUT” HTTP verb.

To specify index body, we need to specify index settings, we need to add a request body. That’s done by adding a JSON object on the next line.

The first line specifies the HTTP verb and endpoint, while the following lines specifies the JSON request body.

#Creating table with shards

PUT /employee
{
“settings” :{
“number_of_shards” : 1,
“number_of_replicas” : 1
}
}

The “acknowledged” key within the response indicates whether or not the index was successfully created.

The shard is the unit at which Elasticsearch distributes data around the cluster. Replica shard is the copy of primary Shard , to prevent data loss in case of hardware failure.

For indices that you create for production purposes, you should stick to the default values unless you have a reason for not doing so.

#Creating table with mappings/columns

PUT /employee
{
“mappings”: {
“properties”: {
“userid”: {
“type”: “integer”
},
“username”: {
“type”: “text”
},
“mob_number” :{
“type”:”integer”
}
}
}
}

#Adding mappings into indices

POST /employee/_doc
{
“userid” : 1,
“username” : “Deepak”,
“mob_number” : 1212121212
}

#Adding values into indices using particular id

PUT /employee/_doc/100
{
“userid” : 2,
“username” : “Atrahe”,
“mob_number” : 9898989898
}

#Get all the data in an index

GET /employee/_search?pretty
{
“query”: {
“match_all”: {}
}
}

#Get data by id

GET /employee/_doc/100

#update particular attribute in elastic

POST /employee/_update/{id}
{
“doc” : {
“mob_number” : 2323232323
}
}

#add one more property into existing index

POST /employee/_update/{id}
{
“doc” : {
“tags” : [“elastic”]
}
}

#update particular value of a property

POST /employee/_update/{id}
{
“script” : {
“source” : “ctx._{mapping_name} = {value}”
}
}

#get all the data in an index

GET /employee/_search?pretty
{
“query”: {
“match_all”: {}
}
}

#to delete an index

DELETE /employee
