# ooHoverboardFirmware
 object oriented hoverboard firmware

original firmware hack https://github.com/NiklasFauth/hoverboard-firmware-hack modified to conpile as c++ code :-)

main.c contains test code:

```class Point;

class Point {
public:
    int x, y;

    Point (int c1, int c2) { x = c1; y = c2;}
    Point& operator=(Point rhs) {
        x = rhs.x; y = rhs.y;
        return *this;
    }
};

class Complex : public Point {
  private: 
    int &real, &imag;
  public: 
    Complex(int r, int i) : Point (r, i), real (x), imag (y) 
    {
    	
    }

};
```

You can compile this repo with my online compiler https://pionierland.de/hoverhack/index.php

But nothing happens when you flash the firmware onto the hoverboard controller :-/

# Ideas welcome !
