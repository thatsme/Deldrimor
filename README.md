Deldrimor
=========

Websocket Server -> Couchbase | Python % Autobahn


This is an implementation of Autobahn framework for interfacing Couchbase throught websocket.

Server side : 

./python -c /yourinstallationpath/server.py

./python -c /yourinstallationpath/client.py -c rpc.couchbase.backend.Component

Client side : 

  Html/Javascript client
  
  Html source

  must include : 
  
      <script src="https://autobahn.s3.amazonaws.com/autobahnjs/latest/autobahn.min.jgz"></script>
      <script src="frontend.js"></script>

  Javascript file
  
  frontend.js
  
  <code>
  
    try {
      var autobahn = require('autobahn');
    } catch (e) {
      // when running in browser, AutobahnJS will
      // be included without a module system
    }

    var connection = new autobahn.Connection({
      url: 'ws://120.0.0.1:9000/',
      realm: 'myrealm'}
    );

    connection.onopen = function (session) {

    session.call('com.couchbase.listdoc',['mydb']).then(
      function (listdoc) {
         console.log("List of documents on db:", listdoc);
         alert(listdoc);
         connection.close();
      },
      function (error) {
         console.log("Call failed:", error);
         alert(error);
         connection.close();
      }
    );
    };

    connection.open();
  
<code/>


