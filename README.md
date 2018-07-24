# ioc_deploy #
These scripts create a portable deployment of an areaDetector plugin that was previously compiled locally. The script copies all of the
important files from the local installation into a given target directory, and creates an envPaths file that directs the IOC to use the
files in this new directory. It may also change the EPICS variable PREFIX in the st.cmd file of the IOC.

## Requirements ##
- ADSupport, ADCore, and the plugin to be copied must be compiled already.
- The EPICS modules that these plugins depend on must be compiled already.
  - asyn, autosave, busy, calc, seq, sscan, iocStats
- EPICS base must be compiled already
- When using absoluteFullDeploy, the envPaths file uses absolute paths; thus, moving the deployment will break the IOC unless the envPaths file is modified. (fullDeploy uses relative paths to avoid this)

## Usage ##
It is highly reccomended to use the fullDeployment script, which copies the necessary files and can add plugins with the envPaths file 
fully configured. Before using any of the scripts, it is necessary to define the BASE, DETECTOR, and SUPPORT macros which define the path 
to EPICS base, areaDetector, and EPICS modules, respectively. The TARGET macro, which defines the location of the deployment, and the
PREFIX macro, which defines the new prefix for the IOC to use, may also be defined in the script or passed as a command line argument
(the command line argument has priority over the value in the script). TARGET must always be the first argument, and PREFIX the second.
Then simply run the script from bash and it will search for and copy the files automatically, and the addPlugin/fullDeployment scripts
will prompt for the name of the plugin to add. 
