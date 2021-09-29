Docker Base Images
==================

Create a new docker base image for use in other projects such as
[router](../router/).

For instance bump Erlang/OTP release to latest revision/fix by revising
`FROM` line within [Dockerfile](builder-erlang/Dockerfile):

- `FROM erlang:23.2.5-alpine as builder` to
- `FROM erlang:23.3.4.5-alpine as builder`

Create new image:

1. Create new branch in git;
   e.g., `esl-release-23.3.4.5`
1. Run `docker` from within local subdirectory containing `Dockerfile`:
   + `cd builder-erlang/`
1. Build a new image locally from command-line:
   + Also "tag" that build similarly to what Dockerfile expects
   + Bump the tagged version number; e.g., from 1 to 2 in our case
   + `docker build --tag heliumsystems/builder-erlang:2 .`
1. Confirm new image exists:
   + `docker images heliumsystems/builder-erlang`
   + Note its "IMAGE ID" value for confirmation below; e.g., abc123...
1. Revise FROM statement within relevant Dockerfiles of other repo:
   + Change the value after the colon
   + e.g., within [Dockerfile-local](../router/Dockerfile-local):
     `FROM heliumsystems/builder-erlang:2`
   + Be sure to change all variations of `Dockerfile*`
1. Build locally as [usual](../router/Makefile), and `docker` will discover
   this newly tagged version in your local cache:
   + Nothing needs to be pushed into any docker repo yet
   + Because it exists within your local cache, the `heliumsystems` docker
     repo never gets queried on this build
   + e.g., `make docker-build`
   + Confirm output from that command has matching IMAGE ID from earlier;
     e.g.,  
     `Step 1/21 : FROM heliumsystems/builder-erlang:2`  
     `---> abc123...`
1. When local testing has been successful, then and only then push the
   image to docker repo
