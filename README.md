#Performance Test Results

##CPU Model:
```
$ cat /proc/cpuinfo | grep "model name" | cut -d: -f2
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
```

##Compiling:
```
$ gcc -O2 -Wall -Wextra -ansi -pedantic MODBUS_CRC16.c -o MODBUS_CRC16
```

##Measuring Algorithm 1 Execution Time:
```
$ time ./MODBUS_CRC16 1 1000000
real	0m22.606s
user	0m22.598s
sys	0m0.005s
```

##Measuring Algorithm 2 Execution Time:
```
$ time ./MODBUS_CRC16 2 1000000
real	0m17.392s
user	0m17.389s
sys	0m0.004s
```

##Measuring Algorithm 3 Execution Time:
```
$ time ./MODBUS_CRC16 3 1000000
real	0m2.443s
user	0m2.441s
sys	0m0.002s
```
