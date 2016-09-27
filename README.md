## Introduction
FakeS3 is a lightweight server that responds to the same calls Amazon S3 responds to.
It is extremely useful for testing of S3 in a sandbox environment without actually
making calls to Amazon, which not only require network, but also cost you precious dollars.

The goal of Fake S3 is to minimize runtime dependencies and be more of a
development tool to test S3 calls in your code rather than a production server
looking to duplicate S3 functionality.  Trying RiakCS, ParkPlace/Boardwalk, or
Ceph might be a place to start if that is your goal.

FakeS3 doesn't support all of the S3 command set, but the basic ones like put, get,
list, copy, and make bucket are supported.  More coming soon.

## Installation

    gem install fakes3

## Running

To run a fakes3 server, you just specify a root and a port.

    fakes3 -r /mnt/fakes3_root -p 4567

## Important note

For any bucket that has a name which can be used as subdomain (no underscores or capital letters, see: http://stackoverflow.com/questions/7111881/what-are-the-allowed-characters-in-a-sub-domain), the AWS V2 SDK will make requests using the buckets name as a subdomain. This means you'll need to be able to route requests for that subdomain to localhost. You can do this by adding the following to /etc/hosts:

127.0.0.1 my-example-bucket.localhost

On CircleCI, there's a handy option for adding host entries: https://circleci.com/docs/configuration/#hosts

If you want to be able to create arbitrary buckets in fake-s3 without editing /etc/hosts, you'll need to setup wildcard subdomains for localhost with something like dnsmasq.

## Connecting to FakeS3

Take a look at the test cases to see client example usage.  For now, FakeS3 is
mainly tested with s3cmd, aws-s3 gem, and right_aws.  There are plenty more
libraries out there, and please do mention if other clients work or not.

Here is a running list of [supported clients](https://github.com/jubos/fake-s3/wiki/Supported-Clients "Supported Clients")

## Running Tests

There are some pre-requesites to actually being able to run the unit/integration tests

### On OSX

Edit your /etc/hosts and add the following line:

    127.0.0.1 posttest.localhost

Then ensure that the following packages are installed (boto, s3cmd)

    > pip install boto
    > brew install s3cmd


Start the test server using

    rake test_server

Then in another terminal window run

    rake test

It is a still a TODO to get this to be just one command

## More Information

Check out the [wiki](https://github.com/jubos/fake-s3/wiki)

[![Join the chat at https://gitter.im/jubos/fake-s3](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jubos/fake-s3?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
