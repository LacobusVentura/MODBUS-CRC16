# Performance Test Results

## CPU Model:
```
$ cat /proc/cpuinfo | grep "model name" | cut -d: -f2
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz
```

## Compiling:
```
$ gcc -O2 -Wall -Wextra -ansi -pedantic MODBUS_CRC16.c -o MODBUS_CRC16
```

## Algorithm 1:
```
static uint16_t MODBUS_CRC16_v1( const unsigned char *buf, unsigned int len )
{
	uint16_t crc = 0xFFFF;
	unsigned int i = 0;
	char bit = 0;

	for( i = 0; i < len; i++ )
	{
		crc ^= buf[i];

		for( bit = 0; bit < 8; bit++ )
		{
			if( crc & 0x0001 )
			{
				crc >>= 1;
				crc ^= 0xA001;
			}
			else
			{
				crc >>= 1;
			}
		}
	}

	return crc;
}
```

### Measuring Algorithm 1 Execution Time:
```
$ time ./MODBUS_CRC16 1 1000000
real	0m22.606s
user	0m22.598s
sys	0m0.005s
```

## Algorithm 2
```
static uint16_t MODBUS_CRC16_v2( const unsigned char *buf, unsigned int len )
{
	static const uint16_t table[2] = { 0x0000, 0xA001 };
	uint16_t crc = 0xFFFF;
	unsigned int i = 0;
	char bit = 0;
	unsigned int xor = 0;

	for( i = 0; i < len; i++ )
	{
		crc ^= buf[i];

		for( bit = 0; bit < 8; bit++ )
		{
			xor = crc & 0x01;
			crc >>= 1;
			crc ^= table[xor];
		}
	}

	return crc;
}
```

### Measuring Algorithm 2 Execution Time:
```
$ time ./MODBUS_CRC16 2 1000000
real	0m17.392s
user	0m17.389s
sys	0m0.004s
```

## Algorithm 3
```
```

### Measuring Algorithm 3 Execution Time:
```
$ time ./MODBUS_CRC16 3 1000000
real	0m2.443s
user	0m2.441s
sys	0m0.002s
```
