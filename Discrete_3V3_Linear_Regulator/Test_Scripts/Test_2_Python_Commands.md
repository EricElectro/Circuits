# Test 2 - Load-Step Transient Response

**Python Inputs**

```python
import pyvisa

# force pure-Python backend
rm   = pyvisa.ResourceManager("@py")     

# open Rigol DG1022Z function generator
gen = rm.open_resource('USB0::6833::1602::DG1ZA262102733::0::INSTR')
scope = rm.open_resource('USB0::6833::1230::DS1ZA269M00391::0::INSTR')

# Configure Oscilloscope Channels for capturing transient response

## Enable Channels 1 and 2
scope.write(':CHAN1:DISP ON')  # Enable Channel 1
scope.write(':CHAN2:DISP ON')  # Enable Channel 2

## Set Channel 1 to measure input pulse (voltage step)
scope.write(':CHAN1:SCAL 1')    # Set vertical scale to 1


# Configure function generator to output 5 V DC on Channel 1
gen.write(':SOUR1:APPL:DC 1,1,5') # 5 V DC on CH1

# Configure function generator to output a pulse waveform on Channel 1
gen.write(':SOUR1:APPL:PULS 20,5,2.5,0') # 5 V pulse on CH1
gen.write('SOUR1:FUNC:PULS:PER 0.05 ') # 50 ms period
gen.write(':SOUR1:FUNC:PULS:DCYC 10') # 10% duty cycle

# Turn on output on Channel 1
gen.write(':OUTP1:STAT ON')

# Turn off output on Channel 1 after testing
# gen.write(':OUTP1:STAT OFF')

```