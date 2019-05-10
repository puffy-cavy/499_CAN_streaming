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
The installation is indicated in https://github.com/commaai/openpilot-tools
(Even though the official github says mentioned the dependencies for Mac, the environment is more friendly with Ubuntu 16.04)
Make sure install the requirements for both Openpilot and Openpilot-tools.
## OPERATION
1. As indicated in Openpilot-tools, in order to stream the CAN messages to EON, you need pre-existing logger files. Openpilot provides a one-minute logger file they recorded when the vehicle running highway straightly. Which can be retrieved from https://github.com/commaai/comma2k19/tree/master/Example_1/b0c9d2329ad1606b%7C2018-08-02--08-34-47
I saved this logger file in the directory: unlogger_data
However, this logger file is not enough to simulate all the traffic conditions for EON. More logger files are needed in the future.
2. The minor changes I made to this project: 
  a) I changed the Openpilot debug UI from vertical view to horizontal view so that it can be displayed on laptop.
  b) 

## TODO

## Clarifications
1. The Openpilot and Openpilot-tools directories in this file is a few commits behind the current official repo. (I cloned the two January 2019) It seems that the development group just added a few features to the current repos, but they shouldn't affect the main functionaily.
2. 
