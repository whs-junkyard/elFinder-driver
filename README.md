# Drivers for elFinder

This is a collection of drivers for [elFinder](https://github.com/Studio-42/elFinder) written by me.

All drivers are licensed under Apache License 2.0.

Drivers are developed under Kyou project. Kyou's development is sponsored
by NECTEC under [National Software Competition 2013](http://fic.nectec.or.th/nsc15/) program.
NECTEC does not provide support for any drivers.

## elFinderVolumeMongoGridFS

Driver for MongoDB's GridFS. **Requires Mongo driver version 1.3.0 and above.**

`fopen` command will returns a MongoGridFSFile resource that could be used as
an ordinary file (read/seek/etc.), but does not support writing to.

### Usage

~~~~~php
require_once 'elfinder/php/elFinder.class.php';
require_once 'elfinder/php/elFinderVolumeDriver.class.php';
require_once 'elfinder-driver/elFinderVolumeMongoGridFS.class.php';
$mongo = new MongoClient('mongodb://user:pass@hostname/elfinder');
$elfinder = new elFinder(array(
	'roots' => array(
		array(
			'driver' => 'MongoGridFS',
			'db' => $mongo->elfinder
		)
	)
));
~~~~~
