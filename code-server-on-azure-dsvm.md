# Code-Server

Code-server is to allow remote VS Code on browser. Details can be found in [here](https://github.com/codercom/code-server).

# Set up on Azure 

## Create an Azure VM
An [Azure Data Science Virtual Machine](https://azure.microsoft.com/en-us/services/virtual-machines/data-science-virtual-machines/) is recommended if one wants to benefit from the pre-installed packages dedicated for AI and data science related development. 

To use code-server securely, it is recommended to configure the VM security rules properly. This can be done in the Azure portal, where one can [specify the inbound security with certain rules](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/nsg-quickstart-portal). 

## Download and install

It can be downloaded and installed from the [code-server official website](https://github.com/codercom/code-server/releases). NOTE at the moment only Linux and Mac OS are supported.

## Run it

The binary of code-server can be run directly from the command line. 

There are several useuful options to run the command, i.e., `--password` allows one to specify the password to login the remote session of VS Code.

