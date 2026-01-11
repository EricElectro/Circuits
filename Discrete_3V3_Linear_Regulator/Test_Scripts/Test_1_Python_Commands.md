# Test 1 - DC Regulation

**Python Inputs**

```python
import pyvisa

# force pure-Python backend
rm   = pyvisa.ResourceManager("@py")     

# open Rigol DG1022Z function generator
gen = rm.open_resource('USB0::6833::1602::DG1ZA262102733::0::INSTR')

# Configure function generator to output 5 V DC on Channel 1
gen.write(':SOUR1:APPL:DC 1,1,5') 

# Turn on output on Channel 1
gen.write(':OUTP1:STAT ON')

# Turn off output on Channel 1 after testing

# gen.write(':OUTP1:STAT OFF')

```