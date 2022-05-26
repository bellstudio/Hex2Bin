# h2bNh

This is Covnering the Interl Hex format file to `Binary` or `C header`  
Support `Extended Segment Address Record` and `Extended Linear Address Record`  

## Convert Intel Hex format file to `Binary` file(s) and `c` header file
### Examples  
<1> For pure hex(without segment):  
```
  python h2bNh.py -f file.hex -a 0x8000 -s 0x3800 -p 0xFF
  This command will generate files starting from address 0x8000, and padding data 0xFF to address(0x8000 + 0x3800) if the hex file address range is less than that.
```
<2> For segment included hex:  
```
  python h2bNh.py -f file.hex --gapSimSeg 64
  This command will generate files according to the address segments, and automantically split data into different binary files(arrays in c header file) if address difference is larger than 64.
```

```c
Default:
align='16', baseAddr='0x0', filename='', gapSimSeg='0', pad='0xFF', sigmentTargetSize='0x0', wcrc=false
```

### Usage:
```
h2bNh.py [-f [File Name]] [-a [Segment Base Address]] [-p [Padded Value]]  
          [--gapSimSeg [Gap to a New Segment]]  
          [-s [The Generated Size of a Sigment]]  
          [--align [Text Align]] [--wcrc] [-h] [-v] 
```

### *Optional arguments*
```
-h, --help            show this help message and exit
-v, --version         show version
-f [File Name], --filename [File Name]
                      where the 'hex' file will be load
-a [Segment Base Address], --baseAddr [Segment Base Address]
                      Used to appoint the Segment base address (will be
                      ignore if has EXT_SIGMENT_ADDR record)
-s [The Generated Size of a Sigment], --sigmentTargetSize [The Generated Size of a Sigment]
                      Padded the output file, if this size larger than
                      actual data size(only support single segment, Hex)
-p [Padded Value], --pad [Padded Value]  
                      Padded value(hex) if the size argument is larger than
                      actual data size(will be ignore if size arg is not
                      appointed)
- [Gap to a New Segment], --gapSimSeg [Gap to a New Segment]
                      If Gap length is larger than dedicated(Dec), then
                      simulate a new segment
--align [Text Align]  The text file will added \r every this number(Dec)
--wcrc                Indicate whether write CRC(24) to binary file, only
                      work when <size> large than <actual size> + 3
```
