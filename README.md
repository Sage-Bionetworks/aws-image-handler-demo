# aws-image-handler

## Overview

This document provides a review of a smart image service implementation that relies on AWS and Thumbor.

## Resources

- [AWS Serverless Image Handler]
- [sharp]

## Review

### AWS Serverless Image Handler

#### Requirements

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

#### Deployment

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

#### Demo

Select the stack created. The tab `Outputs` provides the following URLs:

- ApiEndpoint: https://d1aku1o8fc3y2r.cloudfront.net
- DemoUrl: https://d2xjodzm25t98k.cloudfront.net/index.html

<!-- Definitions -->

[AWS Serverless Image Handler]: https://aws.amazon.com/solutions/implementations/serverless-image-handler/
[sharp]: https://sharp.pixelplumbing.com/