-> Only the PID 1 gets to handle the signals.
- The entrypoint need to be in an [exec form](https://docs.docker.com/engine/reference/builder/#exec-form-entrypoint-example) to get the PID 1. If you run your entrypoint in a shell form (meaning as an argument of /bin/sh), it won't get the PID 1. 
- Once you have your entrypoint running, you can handle the HUP, INT, TERM, and QUIT signals but not the KILL. I tried with nobody and root users inside the container. The trapped signals react as expected but not the KILL one (does not seem to be catchable)
- Note the timestamp at the begining of the file. This can have its importance if you are doing a backup or a logging activity. The trap action is executed as soon as it is read. So if it refers to something that does not exist at the moment the instruction is passed but will be when the trapped is used (signal caught), there might be a problem.
