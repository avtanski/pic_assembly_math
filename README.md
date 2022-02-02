
Multibyte Arithmetic Assembly Library for PIC Microcontrollers
==============================================================

This is a lightweight math library for 8-bit PIC microcontroller projects that require basic multi-byte
arithmetical operations - addition, subtraction, multiplication, and division. The number of bytes for the
operands is configurable.

The library supports the following operations:

* Multibyte addition and subtraction
* Multibyte multiplication
* Multibyte division and modulus (remainder)
* Logical operations (multibyte increment, decrement, rotation to the left and right, clear)
 	
All operations are performed using three N-byte registers, as shown below. (Note: In memory, the registers are
ordered with the least significant byte coming first.)

```
REG_X  	byte N-1	...	byte 2	byte 1	byte 0
REG_Y  	byte N-1	...	byte 2	byte 1	byte 0
REG_Z  	byte N-1	...	byte 2	byte 1	byte 0
```

The library has been tested with PIC16F688 microcontroller, but there is no reason why it shouldn't work on any
8-bit Microchip microcontroller.

To change the register size (number of bytes) adjust the ``PRECISION`` parameter in the beginning of ``math.asm``.


Detailed descriptions of the subroutines
----------------------------------------

The list below contains usage information and details for each subroutine.

* ``M_ADD`` **X + Z -> Z**

  Calculate the sum of registers Z and X. Result is stored back in register Z.
 
* ``M_SUB``	**Z - X -> Z**
 
  Subtract register X from register Z. Result is stored back in register Z.
 
* ``M_MUL``	**X * Y -> Z**
 
  Multiply register X with register Y. Result is stored in register Z.
 
* ``M_DIV``	**Z / X -> Y; Z mod X -> Z**
 
  Divide register Z by register X. Result is stored in register Y. Remainder (modulus) of the division is
  stored in register Z.
 
* ``M_CMP`` **Z <=> X -> STATUS**
 
  Compare registers Z and X. Comparison results are returned in the STATUS register. If register Z==X,
  the Z-bit of the STATUS register is set. If register Z=>X, the C-bit of the STATUS register is set.

* ``M_INC`` **REG + 1 -> REG**
 
  Increment a register. The address of the register is passed to the subroutine in WREG. For example, to
  increment the X register, store REG_X's address in WREG and call M_INC:
 
  ```
    movlw   REG_X
    call    M_INC
  ```

* ``M_DEC`` **REG - 1 -> REG**
 
  Decrement a register. The address of the register is passed to the subroutine in WREG.
  For example, to decrement the Y register, store REG_Y's address in WREG and call M_DEC:

  ```
    movlw   REG_Y
    call    M_DEC
  ```
  
* ``M_ROL`` **REG << 1 -> REG**
 
  Rotate a register to the left. The address of the register is passed to the subroutine in WREG.
  For example, to rotate the Z register, store REG_Z's address in WREG and call M_ROL:

  ```
    movlw   REG_Z
    call    M_ROL
  ```
  
* ``M_ROR`` **REG >> 1 -> REG**
 
  Rotate a register to the right. The address of the register is passed to the subroutine in WREG.
  For example, to rotate the X register, store REG_X's address in WREG and call M_ROR:

  ```
    movlw   REG_Z
    call    M_ROR
  ```
  
* ``M_TEST``
 
  A test subroutine. You can run the program in a debugger to experiment with the different subroutines.
 	

If you only need some of the operations listed above, you can generate a customized version of this
library that includes required operations and their dependencies only, by visiting the project site
http://avtanski.net/projects/math/ .
