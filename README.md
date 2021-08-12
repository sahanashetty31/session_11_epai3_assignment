
# Session 11

# Iterables and Iterators - I 

**Project: Description**

The starting point for this project is the Polygon class and the Polygons sequence type we created in the previous project.

The code for these classes along with the unit tests for the Polygon class are below if you want to use those as your starting point. But use whatever you came up with in the last project.

**ONLY Goal**

Refactor the Polygons (sequence) type, into an iterable. You'll need to implement both an iterable, and an iterator.

```python
class Polygons:
    def __init__(self, m, R):
        if m < 3:
            raise ValueError('m must be greater than 3')
        self._m = m
        self._R = R
        self._polygons = [Polygon(i, R) for i in range(3, m+1)]

    def __len__(self):
        return self._m - 2

    def __repr__(self):
        return f'Polygons(m={self._m}, R={self._R})'

    def __getitem__(self, s):
        return self._polygons[s]

    def __iter__(self):
        return self.PolygonIterator(self)

    @property
    def max_efficiency_polygon(self):
        sorted_polygons = sorted(self._polygons,
                                 key=lambda p: p.area/p.perimeter,
                                reverse=True)
        return sorted_polygons[0]

    class PolyIterator:
        def __init__(self, poly_obj):
            self._poly_obj = poly_obj
            self._index = 0

        def __iter__(self):
            return self


        def __next__(self):
            if self._index >= len(self._poly_obj):
                raise StopIteration
            else:
                item = self._poly_obj._polygons[self._index]
                self._index += 1
                return item
```


## **Test cases**

* `__len__`

  Returns length of an object.

* `__repr__` 

  Returns a string containing a printable representation of an object.

* `__getitem__`

   The method `__getitem__(self, key)` defines behavior for when an item is accessed, using the notation self[key].

* `__iter__`

  An iterable object is an object that implements `__iter__`, which is expected to return an iterator object. 

* `__next__`

  An iterator is an object that implements `__next__`, which is expected to return the next element of the iterable object that returned it, and raise a StopIteration exception when no more elements are available.
  






