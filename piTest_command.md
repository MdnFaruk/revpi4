# RevPi Connect 4 - Complete piTest Commands Reference

## System Information Commands

```bash
# Get device list with addresses
piTest -d

# Get system version
piTest -V

# Check RevPi status and temperature
piTest -r RevPiStatus          # System status
piTest -r Core_Temperature     # Core temperature
piTest -r Core_Frequency       # Core frequency
piTest -r RevPiIOCycle         # I/O cycle time
```

## DIO Module Commands (Address: 32)

### Digital Input Reading
```bash
# Read individual digital inputs (I_1 to I_16)
piTest -r I_1                  # Read digital input 1
piTest -r I_2                  # Read digital input 2
piTest -r I_3                  # Read digital input 3
piTest -r I_4                  # Read digital input 4
piTest -r I_5                  # Read digital input 5
piTest -r I_6                  # Read digital input 6
piTest -r I_7                  # Read digital input 7
piTest -r I_8                  # Read digital input 8
piTest -r I_9                  # Read digital input 9
piTest -r I_10                 # Read digital input 10
piTest -r I_11                 # Read digital input 11
piTest -r I_12                 # Read digital input 12
piTest -r I_13                 # Read digital input 13
piTest -r I_14                 # Read digital input 14
piTest -r I_15                 # Read digital input 15
piTest -r I_16                 # Read digital input 16

# Read all inputs at once using offset (16 bits = 2 bytes)
piTest -r 0,2,h                # Read all 16 digital inputs as hex
piTest -r 0,2,b                # Read all 16 digital inputs as binary
```

### Digital Output Control
```bash
# Write to individual digital outputs (O_1 to O_16)
piTest -w O_1,1                # Set digital output 1 HIGH
piTest -w O_1,0                # Set digital output 1 LOW
piTest -w O_2,1                # Set digital output 2 HIGH
piTest -w O_3,1                # Set digital output 3 HIGH
piTest -w O_4,1                # Set digital output 4 HIGH
piTest -w O_5,1                # Set digital output 5 HIGH
piTest -w O_6,1                # Set digital output 6 HIGH
piTest -w O_7,1                # Set digital output 7 HIGH
piTest -w O_8,1                # Set digital output 8 HIGH
piTest -w O_9,1                # Set digital output 9 HIGH
piTest -w O_10,1               # Set digital output 10 HIGH
piTest -w O_11,1               # Set digital output 11 HIGH
piTest -w O_12,1               # Set digital output 12 HIGH
piTest -w O_13,1               # Set digital output 13 HIGH
piTest -w O_14,1               # Set digital output 14 HIGH
piTest -w O_15,1               # Set digital output 15 HIGH
piTest -w O_16,1               # Set digital output 16 HIGH

# Read output status
piTest -r O_1                  # Read current state of output 1
piTest -r Output_Status,h      # Read all output states as hex
```

### PWM Control
```bash
# Set PWM values (0-255 for 8-bit PWM)
piTest -w PWM_1,128            # Set PWM output 1 to 50% duty cycle
piTest -w PWM_2,255            # Set PWM output 2 to 100% duty cycle
piTest -w PWM_3,64             # Set PWM output 3 to 25% duty cycle
piTest -w PWM_4,192            # Set PWM output 4 to 75% duty cycle
piTest -w PWM_5,0              # Set PWM output 5 to 0% (off)

# Read PWM values
piTest -r PWM_1                # Read current PWM value for output 1
piTest -r PWM_2                # Read current PWM value for output 2

# Set PWM frequency (affects all PWM outputs)
piTest -w OutputPWMFrequency,10  # Set PWM frequency (1-255)

# Enable/disable PWM mode for specific outputs (bitfield)
piTest -w OutputPWMActive,1    # Enable PWM on output 1 only
piTest -w OutputPWMActive,3    # Enable PWM on outputs 1 and 2 (binary: 11)
piTest -w OutputPWMActive,255  # Enable PWM on outputs 1-8
```

### Counter Functions
```bash
# Read counter values (32-bit counters)
piTest -r Counter_1            # Read counter 1 value
piTest -r Counter_2            # Read counter 2 value
piTest -r Counter_3            # Read counter 3 value
piTest -r Counter_4            # Read counter 4 value
piTest -r Counter_5            # Read counter 5 value
piTest -r Counter_6            # Read counter 6 value
piTest -r Counter_7            # Read counter 7 value
piTest -r Counter_8            # Read counter 8 value
piTest -r Counter_9            # Read counter 9 value
piTest -r Counter_10           # Read counter 10 value
piTest -r Counter_11           # Read counter 11 value
piTest -r Counter_12           # Read counter 12 value
piTest -r Counter_13           # Read counter 13 value
piTest -r Counter_14           # Read counter 14 value
piTest -r Counter_15           # Read counter 15 value
piTest -r Counter_16           # Read counter 16 value

# Reset specific counters (bitfield: bit 0 = counter 1, bit 1 = counter 2, etc.)
piTest -R 32,0x0001            # Reset counter 1 (bit 0)
piTest -R 32,0x0002            # Reset counter 2 (bit 1)
piTest -R 32,0x0004            # Reset counter 3 (bit 2)
piTest -R 32,0x0008            # Reset counter 4 (bit 3)
piTest -R 32,0x0003            # Reset counters 1 and 2
piTest -R 32,0xFFFF            # Reset all counters
```

### DIO Configuration
```bash
# Configure input modes (0=Digital, 1=Counter, 2=Encoder)
piTest -w InputMode_1,0        # Set input 1 to digital mode
piTest -w InputMode_1,1        # Set input 1 to counter mode
piTest -w InputMode_2,2        # Set input 2 to encoder mode

# Set input debounce time (bitfield for all 16 inputs)
piTest -w InputDebounce,65535  # Enable debounce for all inputs
piTest -w InputDebounce,0      # Disable debounce for all inputs

# Configure output modes (bitfield: 0=Push-pull, 1=Open-drain)
piTest -w OutputPushPull,65535 # Set all outputs to push-pull mode
piTest -w OutputPushPull,0     # Set all outputs to open-drain mode

# Enable/disable open load detection (bitfield)
piTest -w OutputOpenLoadDetect,65535  # Enable for all outputs
piTest -w OutputOpenLoadDetect,0      # Disable for all outputs
```

## AIO Module Commands (Address: 31)

### Analog Input Reading
```bash
# Read analog input values (16-bit signed values)
piTest -r InputValue_1         # Read analog input 1 raw value
piTest -r InputValue_2         # Read analog input 2 raw value
piTest -r InputValue_3         # Read analog input 3 raw value
piTest -r InputValue_4         # Read analog input 4 raw value

# Read input status (error flags)
piTest -r InputStatus_1        # Read input 1 status flags
piTest -r InputStatus_2        # Read input 2 status flags
piTest -r InputStatus_3        # Read input 3 status flags
piTest -r InputStatus_4        # Read input 4 status flags
```

### RTD Temperature Sensor Reading
```bash
# Read RTD temperature values
piTest -r RTDValue_1           # Read RTD sensor 1 value
piTest -r RTDValue_2           # Read RTD sensor 2 value

# Read RTD status
piTest -r RTDStatus_1          # Read RTD sensor 1 status
piTest -r RTDStatus_2          # Read RTD sensor 2 status
```

### Analog Output Control
```bash
# Write analog output values (16-bit values, range depends on configuration)
piTest -w OutputValue_1,0      # Set analog output 1 to minimum
piTest -w OutputValue_1,32767  # Set analog output 1 to maximum positive
piTest -w OutputValue_1,-32768 # Set analog output 1 to maximum negative
piTest -w OutputValue_2,16384  # Set analog output 2 to mid-range

# Read current output values
piTest -r OutputValue_1        # Read current analog output 1 value
piTest -r OutputValue_2        # Read current analog output 2 value

# Read output status
piTest -r OutputStatus_1       # Read analog output 1 status
piTest -r OutputStatus_2       # Read analog output 2 status
```

### AIO Configuration
```bash
# Configure input ranges (0=±10V, 1=0-10V, 2=±5V, 3=0-5V, 4=±20mA, 5=0-20mA, 6=4-20mA)
piTest -w Input1Range,0        # Set input 1 to ±10V range
piTest -w Input1Range,4        # Set input 1 to ±20mA range
piTest -w Input2Range,6        # Set input 2 to 4-20mA range
piTest -w Input3Range,1        # Set input 3 to 0-10V range
piTest -w Input4Range,3        # Set input 4 to 0-5V range

# Configure scaling factors
piTest -w Input1Multiplier,1   # Set input 1 multiplier
piTest -w Input1Divisor,1      # Set input 1 divisor
piTest -w Input1Offset,0       # Set input 1 offset

# Configure output ranges (0=±10V, 1=0-10V, 2=±5V, 3=0-5V, 4=±20mA, 5=0-20mA, 6=4-20mA)
piTest -w Output1Range,0       # Set output 1 to ±10V range
piTest -w Output2Range,4       # Set output 2 to ±20mA range

# Configure output scaling
piTest -w Output1Multiplier,1  # Set output 1 multiplier
piTest -w Output1Divisor,1     # Set output 1 divisor
piTest -w Output1Offset,0      # Set output 1 offset

# Configure slew rate control
piTest -w Output1EnableSlew,1  # Enable slew rate control for output 1
piTest -w Output1SlewStepSize,10  # Set slew rate step size
piTest -w Output1SlewClock,1   # Set slew rate clock in kHz

# RTD sensor configuration (0=PT100, 1=PT1000, 2=NI100, 3=NI1000)
piTest -w RTD1Type,0           # Set RTD 1 to PT100
piTest -w RTD2Type,1           # Set RTD 2 to PT1000

# RTD wiring configuration (0=2-wire, 1=3-wire, 2=4-wire)
piTest -w RTD1Wiring,2         # Set RTD 1 to 4-wire mode
piTest -w RTD2Wiring,1         # Set RTD 2 to 3-wire mode

# ADC data rate (0=50Hz, 1=60Hz, 2=500Hz)
piTest -w ADC_DataRate,0       # Set to 50Hz for highest precision
```

## Continuous Monitoring Commands
```bash
# Monitor multiple values continuously (Ctrl+C to stop)
piTest -r I_1                  # Monitor digital input 1
piTest -r InputValue_1         # Monitor analog input 1
piTest -r Counter_1            # Monitor counter 1
piTest -r Core_Temperature     # Monitor system temperature

# One-time readings (no continuous loop)
piTest -1 -r I_1              # Read digital input 1 once
piTest -1 -r InputValue_1     # Read analog input 1 once

# Quiet mode (values only, no labels)
piTest -q -r I_1              # Read digital input 1 quietly
piTest -q -r InputValue_1     # Read analog input 1 quietly
```

## System Control Commands
```bash
# Stop/restart I/O update
piTest -S                      # Stop I/O update
piTest -S                      # Start I/O update (run again)

# Reset piControl process
piTest -x                      # Reset piControl
piTest -l                      # Wait for piControl reset completion

# Firmware update
piTest --assume-yes --module 31 -f  # Update AIO module firmware
piTest --assume-yes --module 32 -f  # Update DIO module firmware
```

## Bit Manipulation Commands
```bash
# Get specific bits from bytes
piTest -g 0,0                  # Get bit 0 from byte at offset 0
piTest -g 0,7                  # Get bit 7 from byte at offset 0

# Set specific bits in bytes
piTest -s 0,0,1                # Set bit 0 to 1 in byte at offset 0
piTest -s 0,0,0                # Set bit 0 to 0 in byte at offset 0
```

## Usage Examples for Common Tasks

### Example 1: Digital I/O Control
```bash
# Turn on outputs 1-4
piTest -w O_1,1 && piTest -w O_2,1 && piTest -w O_3,1 && piTest -w O_4,1

# Read all digital inputs
piTest -1 -q -r I_1; piTest -1 -q -r I_2; piTest -1 -q -r I_3; piTest -1 -q -r I_4
```

### Example 2: Analog I/O Control
```bash
# Set analog outputs to specific voltages (assuming ±10V range)
piTest -w OutputValue_1,16384  # ~5V output
piTest -w OutputValue_2,-16384 # ~-5V output

# Read all analog inputs
piTest -1 -q -r InputValue_1; piTest -1 -q -r InputValue_2
```

### Example 3: PWM Control
```bash
# Configure PWM on output 1
piTest -w OutputPWMActive,1    # Enable PWM mode
piTest -w PWM_1,128           # Set to 50% duty cycle
piTest -w OutputPWMFrequency,50  # Set frequency
```

## Notes
- All offset values are automatically calculated by PiCtory
- DIO module is at position 32, AIO module at position 31
- Use Ctrl+C to stop continuous monitoring commands
- Values are in raw format; apply scaling factors as needed for real-world units
- For current measurement on AIO, ensure wire bridges are properly installed
- RTD sensors require proper wiring configuration for accurate readings