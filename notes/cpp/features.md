# Features

## Variable unpacking

```cpp
struct Point {
    int x;
    int y;
};

auto [x, y] = Point{1, 2};
```