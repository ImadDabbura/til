```
High address (args and env):
----------------------------
envp[55] at                                            : 0x7FF7BE0AD5D0
environ[55] at                                         : 0x7FF7BE0AD5D0
envp[0] at                                             : 0x7FF7BE0AD418
environ[0] at                                          : 0x7FF7BE0AD418
last arg at                                            : 0x7FF7BE0AD410
first arg at                                           : 0x7FF7BE0AD408

Stack:
------
First variable inside main at                          : 0x7FF7BE0AD294
func_array[] ends at                                   : 0x7FF7BE0AD2C0
func_array[] (like 'array[]', but on stack) begins at  : 0x7FF7BE0AD2B0
argc at                                                : 0x7FF7BE0AD2A8
argv at                                                : 0x7FF7BE0AD2A0
envp at                                                : 0x7FF7BE0AD298
func2 (from main): frame at                            : 0x7FF7BE0AD254
func frame at                                          : 0x7FF7BE0AD258
static int n within func at                            : 0x   101E5A06C
func (called     0 times): frame at                    : 0x7FF7BE0AD258
func2 (from func): frame at                            : 0x7FF7BE0AD234

Shared memory:
--------------
shared memory attachment begins at                     : 0x   101F84000
shared memory attachment ends at                       : 0x   101F9C6A0

Heap:
-----
malloced area ends at                                  : 0x6000026AD120
malloced area begins at                                : 0x6000026AD100

Uninitialized Data (BSS):
-------------------------
Semaphore at                                           : 0x   101E5A0F4
Cond at                                                : 0x   101E5A080
Lock at                                                : 0x   101E5A0B0
array[] ends at                                        : 0x   101E5A080
array[] (uninitialized, fixed-size char * on BSS) from : 0x   101E5A070
num2 (uninitialized global int) at                     : 0x   101E5A0F0
string2 (uninitialized global char *) at               : 0x   101E5A0F8
extern **environ at                                    : 0x7FF8497239A0

Initialized Data:
-----------------
num (initialized global int) at                        : 0x   101E5A068
string (initialized global char *) at                  : 0x   101E5A060

Text Segment:
-------------
func2 (function) at                                    : 0x   101E55440
func (function) at                                     : 0x   101E55470
main (function) at                                     : 0x   101E54F20
```
