---
layout: post
title: Installing GDAL on a Debian Stretch Docker instance
date: '2018-04-02T03:13:00-04:00'
---

I had to get GDAL working in a Docker image with Debian Stretch for circleci. Here's the working dockerfile:

```
FROM circleci/ruby:2.6.0-stretch

# GDAL
# RUN sudo apt-get install -y gdal-bin # Nope -- gets us 2.1
RUN sudo apt-get install -y libproj-dev proj-data proj-bin
RUN sudo apt-get install libgeos-dev -y
RUN sudo wget http://download.osgeo.org/gdal/2.4.1/gdal241.zip
RUN sudo unzip gdal241.zip
RUN sudo sudo chmod o+x gdal-2.4.1
RUN cd gdal-2.4.1 && sudo ./configure --with-pg --with-geos --with-spatialite --with-libkml --with-proj && sudo make -j4 && sudo make install
```
