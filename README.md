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

## elFinderVolumeS3

Driver for Amazon S3. Requires aws.phar which is bundled.

This driver does not support folder larger than 1,000 items, the maximum content length that could be returned from a single request to S3 API.

### Usage

For a list of region names, see http://docs.amazonwebservices.com/general/latest/gr/rande.html#s3_region

For a list of canned ACL, see http://docs.amazonwebservices.com/AmazonS3/latest/dev/ACLOverview.html The default is `private`

To get access key and secret, go to https://portal.aws.amazon.com/gp/aws/securityCredentials

Bucket needs to be created beforehand.

~~~~~php
require_once 'elfinder/php/elFinder.class.php';
require_once 'elfinder/php/elFinderVolumeDriver.class.php';
require_once 'elfinder-driver/elFinderVolumeS3.class.php';
$elfinder = new elFinder(array(
	'roots' => array(
		array(
			'driver' => 'S3',
			"s3" => array(
				"key" => "ASDF",
				"secret" => "asdf",
				"region" => "ap-southeast-1"
			),
			"bucket" => "elfinder",
			"acl" => "private"
		)
	)
));
~~~~~

### Known Issue
Moving file does not work