# Reverse engineering the ANE

There is currently no public API for using the ANE, but there are private frameworks that are used by Core ML. It is possible to figure out how the ANE works -- or at least how to talk to it -- by looking inside these private frameworks.

geohot has published [some initial results](https://github.com/geohot/tinygrad/tree/master/accel/ane) in the tinygrad repo.

Recordings of the live streams where he's figuring how the ANE works:

- https://www.youtube.com/watch?v=H6ZpMMDvB1M
- https://www.youtube.com/watch?v=JAyw7OAcXDE
- https://www.youtube.com/watch?v=Cb2KwcnDKrk
- https://www.youtube.com/watch?v=9LzJ3h9iKEA

There are some interesting Python libraries to interface with the ANE

- ANE compiler: https://pypi.org/project/anecc/
- ANE converter: https://pypi.org/project/anect/
- ANE driver interface: https://pypi.org/project/ane/
