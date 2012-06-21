SVN Log Parser (for Node.js)
============================

The SVN Log Parser module will parse SVN logs as into relevant JSON.


Install as dependency
---------------------

Install the module:

    npm install svn-log-parser

...or...

Add to your `package.json` file:

    {
      "name":        "my-app",
      // ...
      "dependencies": {
        // ...
        "svn-log-parser": "x"
      }
    }


Parsing SVN Logs as a String
----------------------------

Create a new parser and pass it a callback function and a string of SVN logs:

    var parser = require("svn-log-parser");

    parser(function( results ) {
      console.log("files", results.files);
      console.log("revs", results.revs);
    }, svnLogOutput);


Stream all the Things
---------------------

The parser has a streaming interface to allow pipes in and out. The stream will
also emit events as it parses _actions_ and _revisions_.

    var parser = require("svn-log-parser");

    var cleaner = parser();

    cleaner.on("action", function( action ) {
      console.log("action");
    });

    cleaner.on("rev", function( rev ) {
      console.log("rev");
    });

    cleaner.on("end", function( results ) {
      console.log("end");
    });

    process.stdin.pipe(cleaner);
    process.stdin.resume();


License
-------

    * Copyright (c) 2012 Jacob Swartwood
    * Licensed under the MIT license
    * http://jacob.swartwood.info/license/
