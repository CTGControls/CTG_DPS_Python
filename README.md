## Example code showing the python SPI read problem 

At fist I thought the problem with the chip was in the SPI write but, after some investigation the SPI problem is not with the write it is with read back. I am dropping the least significant bit from the byte more often than not. The decoder show the data coming over the wire correct. 

Some reads from AD4116 showing only one good read:
```diff
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
+ get_register: got [ 0x80 0x00 0x55 ] from reg [ 0x30 ] using command [ 0x70  ]
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
- get_register: got [ 0x80 0x00 0x54 ] from reg [ 0x30 ] using command [ 0x70  ] 
```

Siglent SDS 1104x-e Digital Storage Oscilloscope showing the the correct data a commad 0x70 and a read of 0x800055 
![SPI Message](/../main/res/SDS00001.jpg)



I have tested this Metro ESP32-S2 with C (Arduino) and it works without any problems. I have also used a few different Arduino boards without any problems.
