##JugglingDB Adapter for DynamoDB
* Dependencies : `aws-sdk`, `colors`.
* Installation: The adapter has not been published to the npm registry yet. Once a good set of tests are implemented, it will be published to npm registry. For now git clone the repository to the node_modules directory of your compound app. 
* `git clone https://github.com/tmpaul/jugglingdb-dynamodb` or download as zip and paste manually.
* Make sure you have aws-sdk and colors already installed.

### Using the adapter with DynamoDB Local
* During the testing/development phase of your application's lifecycle, it is a good idea to use DynamoDB local. DynamoDB local is a java archive file that runs on your machine, and it does a very good job at mocking the original database. Download the file <a href = "http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest">here.</a>
* To run DynamoDB Local, use this command from the terminal in the directory where you extracted the tar file: `java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar [options]`

### Using the adapter with DynamoDB remote
* Put your AWS access key and secret access key IDs along with the region in `credentials.json` in the root folder of your app. For example, 
```javascript
{ 
  "accessKeyId": "xxxxxxxxxxxxxx", 
  "secretAccessKey": "xxxxxxxxxxxxxxxxxx", 
  "region": "us-east-1" 
}
```
 If this file is missing, the adapter will try to read host, port , IDs and key from the values you pass in the schema/model file. See below for an example.

#### Options: 
* -port port_number (8000 by default) 
* --inMemory (Run in memory).

### Schema file
```javascript
    var dynSettings = {
      host: "localhost",
      port:"8000", 
      accessKeyId: "mykey",
      secretAccessKey:"secret"
    };
```
####Options:
- host: Address of the dynamodb server. Defaults to "localhost".
- port: Port number of the dynamodb server. Defaults to "8000".
- region: DynamoDB server region. Defaults to "ap-southeast-1".
- accessKeyId: Your access key id. Defaults to "fake".
- secretAccessKey: Your secret access key. Defaults to "fake".
- ReadCapacityUnits: Provisioned read throughput. Defaults to 5.
- WriteCapacityUnits: Provisioned write throughput. Defaults to 10.

####Model Definition
```javascript
    schema('dynamodb', dynSettings, function () {
    var User = describe('User', function () {
      property('id', Number, {null:false, keyType:"hash"});
      property('name', String, {default: "Name"});
      property('isHappy', Boolean, {default: "false"});
      property('dob', Date, {default: Date});
      set('restPath', pathTo.users);
      });
    });
```
####Usage
Coming soon.
