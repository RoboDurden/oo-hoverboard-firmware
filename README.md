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

changes in Makefile
```
LIBS = -lc -lc -lrdimon -lnosys	#ROBO

CC = $(PREFIX)g++

AS = $(PREFIX)g++ -x assembler-with-cpp
```

main.c
```
int abs(int i)	//ROBO
{
	if (i<0) return -i;
	return i;
};
```
and three times
`HAL_GPIO_WritePin(OFF_PORT, OFF_PIN,(GPIO_PinState) 0);	//ROBO
`

setup.c
```
extern UART_HandleTypeDef huart2;	//ROBO
extern DMA_HandleTypeDef hdma_i2c2_rx;	//ROBO
extern DMA_HandleTypeDef hdma_i2c2_tx;	//ROBO

```

control.c
```
extern DMA_HandleTypeDef hdma_i2c2_rx;	//ROBO
extern DMA_HandleTypeDef hdma_i2c2_tx;	//ROBO

```` 

comms.c
```
extern UART_HandleTypeDef huart2;	//ROBO

char uart_buf[100];	//ROBO volatile 
int16_t ch_buf[8];	//ROBO volatile 

```

setup.h
```
void setScopeChannel(uint8_t ch, int16_t val);
void consoleScope();

```

 i only had to add the `extern`  and remove the `volatile`
Don't really know what the extern does and am not really happy to have removed the volatile. 

binary sizes:
```
 hover_c++.bin 23.296 bytes
 hover_c.bin 18.260 bytes

```
The flash size of the stm32f103xe is 512 kB :-)
