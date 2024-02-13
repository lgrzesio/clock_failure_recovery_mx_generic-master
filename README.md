
# Description
This script reacts against 19.44Mhz central clock failure issue.
For POST PR1463169 Junos version, the script reacts agaist CHASSISD_CB_19MHZ_CLK_FAIL
Once the alam is generated and JUNOS performes RE switchover, the script switch 19.4Mhz clock selecton on AgentSmith boards.

NOTE: AS board will be reverted to default behavior upon subsequent FPC reboot. Please replace old master CB as soon as possible.

 For PRE PR1463169 Junos version, Once the error is detected, the script performs manual clock switchover on AgentSmith boards then perform RE switchover.

 For POST PR1433948 Junos version, the script does nothing as Junos does perform clock switchover on AS board automatically.
 


# Installation
 Copy this file as /var/db/scripts/event/clock_failure_recovery_mx_gen.slax under both REs.

# Configuration
```
set event-options event-script file clock_failure_recovery_mx_gen.slax
```
# Recommended optional configuration
```
set event-options event-script optional
set system scripts synchronize
```
## For MX480/960, to artificially trigger the clock failure for lab testing (requires root shell access. ) 
NOTE: This way doesn't work on MX240

### To set clock alarm
```
  #spc -w 0 0 0x38 0x85 ; spc -w 0 0 0x39 0xa
```
### To clear clock alarm
```
  #spc -w 0 0 0x38 0x7e; spc -w 0 0 0x39 0x9
```
  
## For MX2010/20120, to artificially trigger the clock failure for lab testing (requires root shell access. ) 

### To set clock alarm
```
  #spc -w 0 0 0x38 0x85 ; spc -w 0 0 0x39 0xa;spc -w 0 0 0x60 0xa0
```

### To clear clock alarm
```
  #spc -w 0 0 0x38 0x7e; spc -w 0 0 0x39 0x9;spc -w 0 0 0x60 0xa1
```

