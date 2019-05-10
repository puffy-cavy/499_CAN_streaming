# 499_CAN_streaming
This is the file to be started with to build the complete simulation of Openpilot on Stunt Rally.
The whole project is divided into three modules: CAN streaming, Workbench and Racing game.
## CAN streaming module
This repo contains all the files needed to stream CAN messages to EON (the dashcam).
Openpilot is the directory forked from https://github.com/commaai/openpilot
This is the self-driving system embedded in EON.
Inside Openpilot directory, clone Openpilot-tools from https://github.com/commaai/openpilot-tools
This directory helps to simulate the periphery connections of a physical car with EON
## SETUP
If you'd like to use Ubuntu with pre-installed dependencies and directories, find the disk image here: 
If you'd like to install the dependencies by yourself, follow the instructions here: 
The installation is indicated in https://github.com/commaai/openpilot-tools
(Even though the official github says mentioned the dependencies for Mac, the environment is more friendly with Ubuntu 16.04)
Make sure install the requirements for both Openpilot and Openpilot-tools.
## OPERATION
1. As indicated in Openpilot-tools, in order to stream the CAN messages to EON, you need pre-existing logger files. Openpilot provides a one-minute logger file they recorded when the vehicle running highway straightly. Which can be retrieved from https://github.com/commaai/comma2k19/tree/master/Example_1/b0c9d2329ad1606b%7C2018-08-02--08-34-47
I saved this logger file in the directory: unlogger_data
However, this logger file is not enough to simulate all the traffic conditions for EON. More logger files are needed in the future.
2. The minor changes I made to this project: 
  * I changed the Openpilot debug UI from vertical view to horizontal view so that it can be displayed on laptop.
  * Instead of *boardd.py* , I created three boardd.py files namded as *boardd_doge.py* and *boardd_original.py* in *openpilot/openpilot_tools/replay/* . *boardd_original.py* and *boardd.py* are the same. *boardd_doge.py* creates an array to store 100 CAN messages and cycles 100 CAN messages to sustain a stable speed for EON. From our experiment, the minimum of CAN messages needed to maintain a relatively stable state for EON is 100.
3. To stream the CAN messages, move unlogger_data to your desired directory, it does not necessarily placed together with Openpilot directory. But make sure you know the file path to *unlogger_data*. 
  * For example: if *unlogger_data* is placed in my home directory (and my user name is wendy), the file path is `home/wendy/unlogger_ata`
4. To start streaming CAN messages:
  * First make sure to connect all the caples with Panda and EON, as indicated in Openpilot repo. Notice that do not turn on the **power** switch on the debugging board before your computer recognizes EON as the connection may not be detected by you computer when the **power** switch is toggled to **ON** (this is a weird problem in my Ubuntu virtual machine). After your computer pops up a window says USB connection is detected, turn on the **power** switch. You can also turn on the **ignt** switch now.
  * Open a terminal, under openpilot_tools directory, input `MOCK=1 replay/boardd.py`. This should generate a line saying `can init done`, which indicates that EON recognize your computer as a car
  * Open another terminal, under openpilot_tools directory, input `python replay/unlogger.py <logger_file name> <logger_file path>`. For example, if I want to stream the the logger files in unlogger_data stored in my home directory, I need to type `python replay/unlogger.py 'b0c9d2329ad1606b|2018-08-02--08-34-47' /home/wendy/unlogger_datad` 

## TODO
1. More CAN messages are needed to simulate different traffic conditions for Openpilot.

## Clarifications
1. The Openpilot and Openpilot-tools directories in this file is a few commits behind the current official repo. (I cloned the two January 2019) It seems that the development group just added a few features to the current repos, but they shouldn't affect the main functionaily.
2. *openpilot/openpilot-tools/cereal* was cloned from its repo and cannot be directly accessed in this repo. Please replace this folder as its official repo.
