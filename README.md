# node-thrift (patched)

This repository is for node-thrift latest release of Apache Thrift, without dependency for npm repositories.

# LICENSE

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements. See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership. The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License. You may obtain a copy of the License at
    
       http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied. See the License for the
    specific language governing permissions and limitations
    under the License.

## Install

    npm install thrift 

## Thrift Compiler

You can compile nodejs sources by running the following:

    thrift --gen js:node thrift_file

## Cassandra Client Example:

Here is a Cassandra example:

    var thrift = require('thrift'),
        Cassandra = require('./gen-nodejs/Cassandra')
        ttypes = require('./gen-nodejs/cassandra_types');

    var connection = thrift.createConnection("localhost", 9160),
        client = thrift.createClient(Cassandra, connection);

    connection.on('error', function(err) {
      console.error(err);
    });

    client.get_slice("Keyspace", "key", new ttypes.ColumnParent({column_family: "ExampleCF"}), new ttypes.SlicePredicate({slice_range: new ttypes.SliceRange({start: '', finish: ''})}), ttypes.ConsistencyLevel.ONE, function(err, data) {
      if (err) {
        // handle err
      } else {
        // data == [ttypes.ColumnOrSuperColumn, ...]
      }
      connection.end();
    });

## Custom client and server example

An example based on the one shown on the Thrift front page is included in the examples/ folder.
