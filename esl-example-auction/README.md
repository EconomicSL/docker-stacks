# esl-example-auction

This Dockerfile contains everything necessary to run the [ESL auction simulation example](https://github.com/EconomicSL/auctions-simulation-example).

The simulation is run through a Jupyter notebook running in the esl-base-docker container.

Build using the following command...

`docker build . -t esl/esl-simulation-example:v0.1`

...then run with the following...

`docker run -p 8888:8888 esl/esl-simulation-example`
