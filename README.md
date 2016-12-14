## About this fork

Not maintained here. Used as a backup  only. See https://github.com/kelyvin/ghost-s3-service/issues/1#issuecomment-254424540 for more info and the latest code updates.

## Ghost S3 Service
Supported Ghost Version >= v0.10.0

This module allows you to read and write images from Amazon S3 instead of
storing them locally.

After installing, new images that you save will use an absolute URL to S3. Any
requests to `/content/images/` will be proxied to S3, so that any previous
images in your blog will not be affected.

## Installation

You will need to have a the custom storage module directly in your project
directory, the easiest way to do this is:

```bash
$ npm install ghost-s3-service
$ mkdir content/storage/ghost-s3
```

Then create a file called `index.js` and insert the following code

```
'use strict';
module.exports = require('ghost-s3-service');
```

## Configuration

Create new IAM User with permissions to get object from that bucket. Save the
`ACCESS_KEY` and `ACCESS_SECRET_KEY`.

In `config.js`, add a `storage` block for each environment.

```javascript
    storage: {
        active: 'ghost-s3',
        'ghost-s3': {
            accessKeyId: 'Put_your_access_key_here',
            secretAccessKey: 'Put_your_secret_key_here',
            bucket: 'Put_your_bucket_name_here',
            region: 'Put_your_bucket_region_here'
        }
    },
```

### Asset host
You can add `assetHost` to your config to specify a virtual host url. This is
most frequently used with a content delivery network (CDN) such as CloudFront,
CloudFlare, or others. The modified `storage` block would be:

```javascript
    storage: {
        active: 'ghost-s3',
        'ghost-s3': {
            accessKeyId: 'ACCESS_KEY',
            secretAccessKey: 'SECRET_ACCESS_KEY',
            bucket: 'S3_BUCKET_NAME',
            region: 'S3_REGION',
            assetHost: 'https://cdn.yourdomain.com/'
        }
    }
```

You can add `assetHost` to your config to specify a virtual host url. For more
information, [read this section](http://docs.aws.amazon.com/AmazonS3/latest/dev/VirtualHosting.html)
in the AWS docs.

## Credits
Huge thanks to [muzix](https://github.com/muzix/ghost-s3) for the original storage adapter and [spanishdict](https://github.com/spanishdict/ghost-s3-compat) for the latest updates. This adapter is a fork of spanishdict's project for the purposes of staying up to date with the latest Ghost versions and attempts to maintian active support. It currently has the latest pull request from [acburdine](https://github.com/spanishdict/ghost-s3-compat/pull/11).
