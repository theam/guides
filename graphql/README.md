# When GraphQL makes sense and when it does not

GraphQL is an amazing technology and everyone wants to use it, but overusing it would be as bad as not using it for the right use cases. Here’s our quick reference guide to decide whether you should use GraphQL or not.

> This guide is a live document and totally open for comments and discussion, so feel free to [send us a Pull Request](https://github.com/theam/guides/compare) or [submit an issue](https://github.com/theam/guides/issues/new) to this repository.

## It makes sense when:

* You want your Client applications to be able to make custom queries and/or want to specify how much data they consume:
    * You have to support many active applications with very different API requirements at the same time (different versions of the same app, many platform-specific apps, many apps that consume the same kind of data in different ways).
    * You might want to adapt your app depending on the device’s Internet bandwidth (i.e. showing less data when the Internet connection gets slower)
* You don’t know how your data is going to be used, so you want to focus on defining a clear contract of what things you can request to the server and the data format
* It’s important for you that you can generate/update automatically all your models based on your Schema
* You can trade some query efficiency for flexibility

# It doesn't make sense when

* You need to fetch other kinds of data instead of JSON (e.g. download a file)
* Handle server errors at HTTP level
* You need caching at resource level or you’re planning to implement a Russian doll caching scheme
* Your user applications always consume the data in the same way and data schemes are stable
* You know exactly how your data is going to be used and want to have an optimized server-side (cached) query
