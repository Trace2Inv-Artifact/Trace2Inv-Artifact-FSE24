# Trace2Inv FSE 2024 Artifact

## Overview

This artifact accompanies the paper titled "Demystifying Invariant Effectiveness for Securing Smart Contracts" and provides the source code along with a complete replication package. The purpose of this artifact is to facilitate the validation and reproduction of the research results presented in the paper. Users can explore the methodologies, execute the provided scripts, and verify the findings by using this carefully prepared package.



## where it can be obtained

The artifact can be accessed in two ways (however, to replicate experiment results, reviewers have to use the Docker image, because due to GitHub file size limitations, some data files are only available in the Docker image):

- GitHub Repository: The primary source code and replication package are available on GitHub. You can clone or download the repository from  https://github.com/jeffchen006/Trace2Inv-Invariant-Study-FSE24.git

- Docker Hub: For a stable version of the artifact, refer to the DockerHub link ([zhiychen597/trace2inv-artifact-fse2024](https://hub.docker.com/repository/docker/zhiychen597/trace2inv-artifact-fse2024/general)), which ensures a preserved version as cited in the paper. 

For results related to the invariant study discussed in the paper, please refer to a separate repository available at [another separate repository](https://github.com/jeffchen006/Trace2Inv-Invariant-Study-FSE24)

For benchmarks used in this paper, please refer to a separate repository available at [another another separate repository](https://github.com/Trace2Inv-Artifact/Trace2Inv-Benchmarks)


## Folder Structure
Below is a detailed overview of the folder structure provided in the artifact, which aids in understanding the roles and functions of each component:


### Source Code Folders
- `Benchmarks_Traces/`: Contains transaction trace data for historical transactions of each benchmark contract.
- `Benchmarks_Txs/`:  Stores historical transaction data for each benchmark contract.
- `constraintPackage/`: Includes scripts and modules for generating invariants.
- `crawlPackage/`: Includes tools for crawling blockchain-related information from sources like EtherScan, TrueBlocks, and Ethereum Archive Node.
- `fetchPackage/`: Responsible for fetching results from debug_traceTransaction and pruning them.
- `main.py`: The main Python script for generating invariants.
- `parserPackage/`: Contains parsing utilities for processing data.
- `settings.toml`: Provides configuration settings for various scripts and tools. It is supposed to be secret and not shared.
- `staticAnalyzer/`: Contains code for analyzing Solidity and Vyper source code to assist invariant generation.
- `trackerPackage/`: Includes tools for dynamic taint analysis.
- `utilsPackage/`: Contains utility scripts and modules supporting various functions.


### Other Tool Folders
- `InvCon+/`: Applies the InvCon+ technique to benchmarks as part of RQ5.
- `TxSpector/`: Applies TxSpector to benchmarks as part of RQ5.


### Cache Folders
- `cache/`: Used for storing analysis results related to benchmarks.
- `crytic-export/`: Acts as a cache folder for Slither, a static analysis tool.
- `data/`: Stores cached data of digested files from the cache folder.


### Artifact-related Files
- `DOCKERFILE`: Defines the Docker container configuration to ensure replicability across different environments.
- `logs.sh`: A script that facilitates the replication process.
- `requirements.txt`: Specifies Python package requirements for proper setup.
- `RQ1RQ3Results/`: Stores results pertaining to research questions 1 and 3.
- `RQ2Study/`: Contains study materials and results for research question 2.
- `RQ4Results/`: Holds results for research question 4.



## How to reproduce the results

### Installation:
This artifact requires users install docker first. 

To install Docker please see one of the following resources
1. [Install Docker for Ubuntu.](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
2. [Install Docker for Mac.](https://docs.docker.com/docker-for-mac/install/)
3. [Install Docker for Windows.](https://docs.docker.com/docker-for-windows/install/)


After installing Docker, please run the following command to pull the docker image from Docker Hub:
```
sudo docker pull zhiychen597/trace2inv-artifact-fse2024:latest
```


### A simple test:
To verify that the Docker image is working correctly, run the following command:
```
./python3.10 main.py AC
```

If the above command executes successfully, the Docker image is functioning correctly. The output should display the following message:
```
RariCapital2_1 has one function call with several transfers
Yearn1 has one function call with several transfers
Eminence has one function call with several transfers
Opyn has one function call with several transfers
...
5 sampled FPs for isOriginManager
len(txList3):  306
```


### Execution:


Step 1: Start a temporary container using the Docker image.
```
sudo docker run -it --rm zhiychen597/trace2inv:latest bash
```


Step 2: Execute Invariant Generation Script
Within the Docker environment, initiate the invariant generation process by executing the logs.sh script:

```
./logs.sh
```
This script automates the generation of invariants across eight categories:

AC - Access Control
TL - Time Lock
GC - Gas Control
RE - Re-Entrancy
SS - Special Storage
OR - Oracle Slippage
DF - DataFlow
MF - MoneyFlow



Results from the execution are stored in respective text files within the `RQ1RQ3Results` directory.


Additionally, this script parses the logs to extract data tables used in the paper. Execute the following commands to parse and save these results to text files, which also display them on the console:

```
python3.10 RQ1RQ3Results/parse.py | tee RQ1RQ3Results/RQ1RQ3-Results.txt
python3.10 RQ2Study/parseTPFP.py | tee RQ2Study/RQ2-Results.txt
python3.10 RQ4/readGas.py | tee RQ4/RQ4-Results.txt
```


These scripts perform the following functions:

- `parse.py`: Parses the results for research questions 1 and 3, producing a summarized output.
- `parseTPFP.py`: Processes the true positives and false positives for the study related to research question 2.
- `readGas.py`: Reads and summarizes gas usage data relevant to research question 4.



Step 3: Check Execution Results

Compare RQ1RQ3Results/RQ1RQ3-Results.txt with RQ1RQ3Results/RQ1RQ3-Expected.txt and Tables 5 & 7 in the paper.

Compare RQ2Study/RQ2-Results.txt with RQ2Study/RQ2-Expected.txt and Table 6 in the paper.

Compare RQ4/RQ4-Results.txt with RQ4/RQ4-Expected.txt and Table 8 in the paper.


For RQ5, raw experimental results are available at InvCon+/results.txt and TxSpector/results.txt. Detailed instructions for running these artifacts can be found at their respective GitHub repositories:
- https://github.com/OSUSecLab/TxSpector
- https://github.com/ntu-SRSLab/InvCon


We hope these steps can guide reviewers and users through the process of validating the artifact and replicating the results presented in the paper.




## Contact Information

Zhiyang Chen (zhiychen@cs.toronto.edu)

<!-- sudo docker build -t trace2inv . -->
<!-- sudo docker run -it trace2inv bash -->