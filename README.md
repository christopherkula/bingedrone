BINGEDRONE
==========

Sometimes we need to binge. Sometimes we must have all the things.

At BINGEDRONE our internationally mysterious fleet of food delivery drones is ready to get you everything you want, and quickly!

Search for your cuisine (or company, or street) to filter the list of SF food trucks, and then hit enter to see the route our drones will fly to bring you ONE OF EVERYTHING you have asked for.

Payment? Don't worry, we'll send a bill. You're good for it.

Live Version On GitHub
----------------------

https://christopherkula.github.io/

To Start BINGEDRONE
-------------------

Kick up your favorite one-line web server from the root directory. We like:

  `ruby -run -ehttpd . -p8000`

Surf over to port 8000 (or whatevz) and be ready to get really, really fat.

Developers
----------

Nothing complicated here. All the logic in app.js.

The drone route is generated in a single pass, using a naïve algorithm:

1) Get the outer bound coordinates of the selected set.
2) Calculate the geographic middle point.
3) Find the truck in the set closest to that point.
4) Work outwards from the "middle" one truck at a time, finding the next closest to either end of the route thus far constructed.

Future Improvements
-------------------

Tests would be nice.

Switch to an unnaïve algorithm for route calculation. The simplest would be a recursive tree of route options, reducing down to the route with the shortest total distance. When there are more than a couple dozen stops, however, an exhaustive search could be computationally draining, so perhaps a hybrid option: start with the current "middle out" system, and use tree comparison to look ahead just a few stops at a time. I think this is when it makes the most boneheaded decisions right now anyway, and constitutes a reasonable compromise in terms of diminishing returns for the BINGEDRONE empire. Definitely needs tests.

Even looking one more hop ahead gets this simple algorithm pretty close to shippable:

<img width="641" alt="faulty route" src="https://github.com/christopherkula/bingedrone/assets/97899131/4a12554d-50b2-40e3-87b1-e13a13645db9">

The ordering of the two stops in the bottom right should be reversed. The route was clearly being built from the "South of Market" neighborhood. From that direction the next hop makes sense, but if the big jump down left were factored in the correct route would have been reached.

UI: It would also be fun to reveal the route quickly but one segment at a time via a timeout mechanism.

