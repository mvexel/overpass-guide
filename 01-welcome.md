Welcome to this beginner's guide to the OpenStreetMap Overpass API!

# What is Overpass?

The Overpass API, or simply Overpass, is a way to get slices of OpenStreetMap data. It was created by Roland Olbricht. If you know Overpass, you can ask OSM questions like:

* Can you show me all the museums in Indonesia?
* Can you show me the roads in Croatia that do not yet have a speed limit?
* Which OSM features in Iran have been most recently edited by OSM user `geoaria`?

In fact, most questions you can think of asking of OSM data can be answered by Overpass in some way or other. And while this guide will not cover the complete power of Overpass, you will learn enough things to satisfy much of your OSM data curiosity.

# Why would I use Overpass?

There are many ways to inspect and query (ask questions of) OSM data. You can download all of OSM for a country or even the world, and use tools like PostGIS or osmium. And these are very powerful tools. But Overpass has some pretty big advantages for most people. First, you don't have to download any data or install any software to use it. Second, Overpass always works on the most current OSM data. And finally, as we will show you in this guide, Overpass is pretty easy to learn.

# Okay, show me an example!

Sure thing!

The easiest way to use Overpass is through a website called Overpass Turbo, created by Martin Raifer.

Let's visit Overpass Turbo by [clicking here](http://overpass-turbo.eu/s/J4r). 

![A screenshot of the Overpass Turbo web site](https://user-images.githubusercontent.com/120452/57871554-cee73680-77c6-11e9-90da-413f6774f53c.jpg)

Overpass Turbo has two main parts. On the left hand side is a text editor, where you enter your question in Overpass language. We call this a *query*. The map on the right will show you the answer to your question as map data.

The editor has the following text in it:

```
node[tourism=museum]({{bbox}});
out meta;
```

This is an Overpass query. Let's look at each of the parts to understand what it means:

* `node`: any line that starts with `node`, `way` or `relation` is called a *query statement*. In this case, we are looking to query *nodes* from OSM.
* `[tourism=museum]`: things in square brackets are called *filters*. Here, we indicate that we are only interested in features that are tagged with `tourism=museum`.
* `({{bbox}})`: the part of the query statement in round brackets is an *area filter*. If a query statement does not have an area filter, you are querying the entire world. Here, we use an area filter that takes the bounding box (`bbox`) of the map on the right hand side: Overpass will only query OSM data in the area visible on the map.
* `;`: The semicolon marks the end of the statement. Overpass will interpret anything after it as a new statement.
* `out meta`: This is an *out statement* and lets Overpass know what data we want back. Here, we tell overpass to output all metadata (`meta`) associated with the OSM data.

If we put all of this together, the question we are asking translates to English as "Overpass, please give me everything OSM knows about all nodes tagged `tourism=museum` that lie inside the map on the right".

Click 'Run' to run this query.

After a few seconds, Overpass comes back with an answer, displayed as dots on the map.