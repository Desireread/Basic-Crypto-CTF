# Basic-Crypto-CTF


## **Target Area: Cryptography**
The purpose of this CTF is to test the participant’s logical thinking, comprehension, and cryptography skills. The CTF requires participants to decode a file giving them hints to the location of the picture containing the flag using base64. Then the participant must find the correct picture, extract the file containing possible flags within, and find the correct flag from within a file containing the encrypted flag. 

## Tools Needed
- base64 - decode directions 
- cat - print the contents of files 
- steghide - extract files from within pictures 
- sha256sum - print out sha256 hash of each flag 
- grep - look for endcoded flags within files 

## Steps to Solve
### 1. Build and Run the Docker Container
a. Download this repository  
b. In the folder conatining the dockerfile, run `docker build -t cryptolab .` to build the container.  
**_Note: "cryptolab" is only a name for the docker container and may be replaced with any name of your choice_**  
c. Once the container is finished, run `docker run -it cryptolab` to start the docker container  
**_Note: the same name used to build the docker conatiner must be used to start the container_**  
### 2. Decode directions.txt
a. Run `base64 -d directions.txt `  

