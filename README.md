# aws-image-handler

## Overview

This document provides a review of a smart image service implementation that relies on AWS and Thumbor.

## Resources

The resources used by [AWS Serverless Image Handler] are listed
[here](https://docs.aws.amazon.com/solutions/latest/serverless-image-handler/resources.html).
The most important resources are introduced below.

- [awslabs / serverless-image-handler](https://github.com/awslabs/serverless-image-handler) (GitHub)

### Amazon CloudFront

[Amazon CloudFront] speeds up distribution of your static and dynamic web content,
such as .html, .css, .php, image, and media files. When users request your
content, CloudFront delivers it through a worldwide network of edge locations
that provide low latency and high performance.

### sharp

[sharp] is a high speed Node.js module is to convert large images in common
formats to smaller, web-friendly JPEG, PNG and WebP images of varying dimensions.

### Thumbor

XXX

### Amazon Rekognition

[Amazon Rekognition] makes it easy to add image and video analysis to your
applications. You just provide an image or video to the Amazon Rekognition API,
and the service can identify objects, people, text, scenes, and activities.
It can detect any inappropriate content as well. Amazon Rekognition also
provides highly accurate facial analysis and facial recognition.

An alternative solution for face detection is to use
[Thumbor custom detection](https://thumbor.readthedocs.io/en/latest/custom_detection.html).

## Requirements

One or more S3 buckets are required to store original images. Let's craete a
bucket and add a picture of a group of people.

- AWS > `S3`
- Click on `Create bucket`
- Bucket name: `aws-image-handler-bucket`
- Click on `Next`
- Click on `Next`
- Check `Block all public access`
- Click on `Next`
- Click on `Create bucket`

Then select the newly created bucket and add a picture of a group of people
named `people.jpg`.

## Deployment

- Go to [AWS Serverless Image Handler]
- AWS > `CloudFormation`
- Click on `Create stack`
    - Click on `Upload a template file`, then upload `serverless-image-handler.template`

        S3 URL: https://s3-us-west-2.amazonaws.com/cf-templates-1d8tw049uftx7-us-west-2/2020230iB3-serverless-image-handler.template

    - Click on `Next`
- Specify stack details
    - Stack name: `aws-image-handler`
    - CorsEnabled: `Yes`
    - SourceBuckets: `aws-image-handler-bucket`
    - AutoWebP: `Yes`
    - Click on `Next`
- Configure stack options
    - Click on `Next`
- Review aws-image-handler
    - Check `I acknowledge that AWS CloudFormation might create IAM resources
      with custom names.`.
    - Click on `Create stack`
- `CloudFormation` > `Stacks` > `aws-image-handler`

## Demo

Select the stack created. The tab `Outputs` provides the following URLs:

- ApiEndpoint: https://d1aku1o8fc3y2r.cloudfront.net
- DemoUrl: https://d2xjodzm25t98k.cloudfront.net/index.html

**Note**:

> The Serverless Image Handler demo UI offers a limited set of image edits and
does not include the full scope of capabilities offered by the Image Handler
API. We recommended using your own front-end application for image modification.

## Filters

The filters supported by Thumbor are documented [here](https://docs.aws.amazon.com/solutions/latest/serverless-image-handler/appendix-d.html).



https://d1aku1o8fc3y2r.cloudfront.net/filters:watermark(aws-image-handler-bucket,sage.png,10,10,1,50)/people.jpg


<!-- Definitions -->

[Amazon CloudFront]: https://docs.aws.amazon.com/cloudfront/index.html
[Amazon Rekognition]: https://docs.aws.amazon.com/rekognition/index.html
[AWS Serverless Image Handler]: https://aws.amazon.com/solutions/implementations/serverless-image-handler/
[sharp]: https://sharp.pixelplumbing.com/