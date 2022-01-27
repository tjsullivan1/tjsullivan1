# Overview

Some commands that I always forget

## Build

build the current directory:

    docker build .

build the current directory and add identifiers:

    docker build . -t file-uploader # create an image named file-uploader, tag will say latest
    docker build . -t file-uploader:0.0.1 # as above, but tag will be 0.0.1
    docker build . -t file-uploader:latest -t file-uploader:0.0.1 # explicit is better than implicit. Addd two tags at once

## Run

run a webapp and port forward for 8000 on local host:
    
    docker run --rm -it -p 8000:80 file-uploader # runs the latest file-uploader

as above, but this time with the bash shel opening:

    docker run --rm -it -p 8000:80 file-uploader /bin/bash

# Images

Each RUN creates an image layer, so consider combining RUN instructions onto one line.
