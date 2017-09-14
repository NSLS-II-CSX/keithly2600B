# keithly2600B
IOC for Keithley 2600B Series SourceMeter Instrument

This ioc is currently under developmemnt.  Signifiant changes will occur.

Initialization commands are currently needed. These are executed using telnet

    `telnet 10.23.3.63 5025`

then enter the commands

200mA i limit (0.2 AMPS)
Keithley inputs/outputs in Amps!
(driving i)
 
or
(driving v)
2V v limit
keither input/output in Volts

``` sh
#commands to input 
#BOOK EXAMPLE with modification  change v and measure I:

###########-- INITIALIZE 
###########-- Restore Series 2600B defaults.
smua.reset()
###########-- Select voltage source function.
smua.source.func = smua.OUTPUT_DCVOLTS
print(smua.source.func)
#should be 1
###########-- Set source range to auto.
smua.source.autorangev = smua.AUTORANGE_ON
###########-- Set voltage source to 5 V.
smua.source.levelv = 5
###########-- Set current limit to 10 mA.
smua.source.limiti = 1e-2
###########-- Set current range to 10 mA.
smua.measure.rangei = 1e-2  
###########-- Turn on output.
smua.source.output = smua.OUTPUT_ON
###########-- Print and place the current reading in the reading buffer.
print(smua.measure.i(smua.nvbuffer1),smua.measure.v(smua.nvbuffer1),smua.measure.r(smua.nvbuffer1))


 
############-- Turn off output.
smua.source.output = smua.OUTPUT_OFF
print(smua.measure.i(smua.nvbuffer1),smua.measure.v(smua.nvbuffer1),smua.measure.r(smua.nvbuffer1))
 
 
##now change i and measure v
smua.reset()
###########-- Select voltage source function.
smua.source.func = smua.OUTPUT_DCAMPS
print(smua.source.func)
#should be 0
###########-- Set source range to auto.
smua.source.autorangei = smua.AUTORANGE_ON
###########-- Set current source to 0.003A.
smua.source.leveli = 3e-3
###########-- Set voltage limit to 6 V.
smua.source.limitv = 6
###########-- Set voltage range to 6 V.
smua.measure.rangev = 6  
###########-- Turn on output.
smua.source.output = smua.OUTPUT_ON
###########-- Print and place the current reading in the reading buffer.
print(smua.measure.i(smua.nvbuffer1),smua.measure.v(smua.nvbuffer1),smua.measure.r(smua.nvbuffer1))

smua.source.leveli = 3e-1
print(smua.measure.i(smua.nvbuffer1),smua.measure.v(smua.nvbuffer1),smua.measure.r(smua.nvbuffer1))
######### measures 1e-1 mA because 
############-- END OF INITIALIZE


############-- A few more controls.
############-- Turn off output.
smua.source.output = smua.OUTPUT_OFF
print(smua.measure.i(smua.nvbuffer1),smua.measure.v(smua.nvbuffer1),smua.measure.r(smua.nvbuffer1))
 
####
#
#  MUCK UP SETTINGS?
smua.reset()
 
###
#
#2 wire, 4 wire, calibrate(for calibration)
print(smua.sense)
# 0 = 2wire
# smua.sense = smua.SENSE_LOCAL
# 1 =  4wire
# smua.sense = smua.SENSE_REMOTE
# 2 = calibration
# smua.sense = smua.SENSE_CALA
 
 
