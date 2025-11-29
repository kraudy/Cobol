# Cobol
Learning Cobol?

# Where to start?

This is the first question i asked to many Cobol developer and the mani answer i got was like: **Get a course from Udemy**. And i was like, Why? Why no one pointed me to someone on youtube with some nice tutorials?

*z16* What is it?


So far, i got enrrolled with https://ibmzxplore.influitive.com/

The ide is **Zowe Explorer**

# Object systems

There is a relation between zos datasets and members to ibm i libraries and members

**PDS**: Partition data sets

Sequeantial datasets are like normal tables with registers
Paritioned datasets are like libraries with members that have registers

So, a dataset is like an object

**JCL** (Job control language) is similar to IBM I **CL** (Control language) in the sense that they are OS specific instrucitons, similar to linux bash commands.

JCL is similar to a CL, where you set up the environmente (files, libraries, overs, etc) before executing a program or just to make the OS do some operations

*job entry subsystem* (JES) may be similar to ibm i Sub systems. When the JCL is submited, it creates a new job (which makes sense) and it is also send to the JES Sub system queue, where it is executed, which also makes sense.

  - **SYSIN** an input file (DD) statement for control commands
  - **SYSPRINT** an output DD statement for the program to report success, failure, progress
  - **SYSUT1** a “source” DD statement where data is to be copied from
  - **SYSUT2** a “target” DD statement where the data from SYSUT1 is to be copied to

This **JCL** thing is nasty stuff.
```bash
//SYSUT2   DD DSN=&SYSUID..JCL3OUT,DISP=(MOD,PASS,DELETE),
//            SPACE=(TRK,(1,1)),UNIT=SYSDA,
//            DCB=(DSORG=PS,RECFM=FB,LRECL=80)
```

A standard **DISP** parameter has three parts. The first parameter is the status, which can be any of the following:
Parameter Meaning
 - **NEW** Create a new data set
 - **SHR** Re-use an existing data set, and let other people use it if they’d like
 - **OLD** Re-use an existing data set, but don’t let others use it while we’re using it
 - **MOD** For sequential data sets only. Re-use an existing data set, but only append new records to the bottom of it. If no data set exists, create a new one.

Field 2 of the DISP parameter describes what should happen to the dataset in the case of a normal jobstep completion, and the third
field is what should happen to the dataset in the case of a jobstep failure.
  - **DELETE** Erase it from storage completely
  - **CATLG** Record the data set so you can use it after the job finishes
  - **PASS** After this step completes, hold on to it so jobsteps that come after this (in the same job) can use it
