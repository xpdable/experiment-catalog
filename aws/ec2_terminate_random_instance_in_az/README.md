# Terminate Random [EC2][ElasticComputeCloud] instance in an [Availability Zone][AvailabilityZone] Chaos Experiment

This experiment explores whether my application can maintain itself when a random [EC2][ElasticComputeCloud] instance is terminated within an [availability zone][AvailabilityZone].

[ElasticComputeCloud]: https://aws.amazon.com/ec2/
[AvailabilityZone]:    https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html

## Setup for Experiment Execution

### Install the Chaos Toolkit

This experiment uses the [free and open source Chaos Toolkit][chaostoolkit]. The instructions for installing the [Chaos Toolkit][chaostoolkit] are available in the [project's documentation][docs].

[chaostoolkit]: https://chaostoolkit.org/
[docs]: https://docs.chaostoolkit.org

### Install Any Required Drivers

The [Chaos Toolkit][chaostoolkit] is extended by adding [drivers]. This experiment requires the following drivers:

* Chaos Toolkit Extension for AWS [aws-driver] [aws-driver-github]

[drivers]: https://docs.chaostoolkit.org/drivers/overview/
[aws-driver]: https://docs.chaostoolkit.org/drivers/aws/
[aws-driver-github]: https://github.com/chaostoolkit-incubator/chaostoolkit-aws

## Running the Experiment

### Required Parameters

This experiment requires the following parameters:

* Environment Variables
  * `APPLICATION_ENTRYPOINT_URL` - Specifies the application entry point URL where your application can be reached in your environment.
  * `AVAILABILITY_ZONE` - The availability zone for the running ec2 instance.

## Running the Experiment Direct from the Catalog using HTTP

You can run this experiment using the native `chaos` command, or using
`docker`.

With the native `chaos` command:

```bash
(chaostk) export APPLICATION_ENTRYPOINT_URL=http://192.168.99.100/myapp; \
          export AVAILABILITY_ZONE=eu-west-2; \
          chaos run https://raw.githubusercontent.com/open-chaos/experiment-catalog/master/aws/ec2_terminate_random_instance_in_az/ec2_terminate_random_instance_in_az.json
```

***NOTE:*** The APPLICATION_ENTRYPOINT_URL and the AVAILABILITY_ZONE should be setup according to your AWS run time environment. The docker command also uses the .chaostoolkit/settings.yaml from the users home directory.

With `docker`:

```bash
$ docker run -it \
           -e APPLICATION_ENTRYPOINT_URL=http://192.168.99.100/myapp \
           -e AVAILABILITY_ZONE=eu-west-2 \
           -v `pwd`:/tmp/result \
           -v ~/.chaostoolkit:/tmp/settings \
            chaostoolkit/chaostoolkit \
           --settings /tmp/settings/settings.yaml \
           chaos run https://raw.githubusercontent.com/open-chaos/experiment-catalog/master/aws/ec2_terminate_random_instance_in_az/ec2_terminate_random_instance_in_az.json
```

### Running the Experiment from a Local Copy

You can run this experiment using the native `chaos` command, or using
`docker`.

With the native `chaos` command:

```bash
(chaostk) export APPLICATION_ENTRYPOINT_URL=http://192.168.99.100/myapp; \
          export AVAILABILITY_ZONE=eu-west-2; \
          chaos run ec2_terminate_random_instance_in_az.json
```

***NOTE:*** The APPLICATION_ENTRYPOINT_URL and the AVAILABILITY_ZONE should be setup according to your AWS run time environment. The docker command also uses the .chaostoolkit/settings.yaml from the users home directory.


With `docker`:

```bash
$ docker run -it \
           -e APPLICATION_ENTRYPOINT_URL=http://192.168.99.100/myapp \
            -e AVAILABILITY_ZONE=eu-west-2 \
           -v `pwd`:/tmp/result \
           -v ~/.chaostoolkit:/tmp/settings \
             chaostoolkit/chaostoolkit \
           --settings /tmp/settings/settings.yaml \
           run ec2_terminate_random_instance_in_az.json
```
