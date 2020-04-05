---
title: "smpl.pk — Building scalable software for the internet"
date: 2019-01-02T16:04:28-05:00
draft: false
---
## Internet scale applications
For my fall semester in 2018, I took a course entitled <a href="https://github.com/thomaspinckney3/cs4501/">Internet Scale Applications</a>. As you might be able to guess, it was a survey of various techniques that software development teams use to build applications that can serve millions (or billions) of users via the internet. For instance, the professor introduced the concept of multi-tiered architectures, NoSQL databases, and microservices.

In order to test our knowledge of the material, we were instructed to build a team of three people and develop a marketplace webapp that would employ a set of techniques we learned in class. Two of our members, including myself, happened to be musicians, therefore when we searched around for inspiration we came across the idea of a _sample pack distribution service_.

## Sample packs
For music producers and sound engineers, a _sample_ could be defined as any clip of audio from one source that is used to create new melodies, beats, and textures. Some examples include single recordings of individual drums or instruments, snippets taken from other songs, or field recordings in nature.

Therefore, any service that offers samples in groups for sale could be called a distribution service for sample packs. One successful business that we took inspiration from was called <a href="https://splice.com">Splice</a>. Splice collaborates with artists and record labels to put out large sample packs that can be purchased with credits earned on a monthly subscription. However, we observed that no marketplace existed where users could conveniently upload their own samples and monetize them as they see fit.

## Technical implementation
This is how our original idea went: individuals upload their samples in a pack, give it a title, description and genre, and set a price on it as they see fit. Users then can browse the marketplace for whatever sounds they need, purchase it for a license to use it however they see fit, and download the sounds for use in a digital audio workstation, for example.

In order to build the app, we set up a Docker-ized Django environment with "web", "experience", "models", and "database" services in individual containers. In order to serve a request, the models microservices fetched information from the database, and returned a JSON response to the experience layer. From there, the experience API tailored this response to the front-end and performed additional validation before giving another JSON response to the web container. In particular, the models service used a RESTful architecture, which made it convenient to call through stateless URL requests.

Some other icing on the cake included an Elasticsearch service and a recommendation system built on Apache Spark. Both used Kafka queueing to allow new listings of sample packs to be indexed asynchronously (with measured performance benefits). We also implemented a Continuous Integration system using Jenkins to schedule unit and integration tests every time a commit was made to the repository.

## For the future
I would like to visit this project at some point and refinish it as a published application for mobile and web environments. As of now, you can check out my team's semester long project <a href="https://github.com/daedrika/smpl-pk/">on Github.</a>
