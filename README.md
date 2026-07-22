# Basic-Crypto-CTF

## **Target Area: Cryptography**
The purpose of this CTF is to test the participant’s logical thinking, comprehension, and cryptography skills. The CTF requires participants to decode a file giving them hints to the location of the picture containing the flag using base64. Then the participant must find the correct picture, extract the file containing possible flags within, and find the correct flag from within a file containing the encrypted flag. 

## Tools Needed
- base64 - decode directions 
- cat - print the contents of files 
- steghide - extract files from within pictures 
- sha256sum - print out sha256 hash of each flag 
- grep - look for endcoded flags within files

## Help
If you get stuck, you can look to any of the following sections in Steps to Solve for hints or guidance:  
[Build and Run the Docker Container](#1-build-and-run-the-docker-container)

## Steps to Solve
### 1. Build and Run the Docker Container
a. Download this repository  

b. In the folder conatining the dockerfile, run `docker build -t cryptolab .` to build the container.  
> [!NOTE]
> "cryptolab" is only a name for the docker container and may be replaced with any name of your choice
>

c. Once the container is finished, run `docker run -it cryptolab` to start the docker container  
> [!Note]
> The same name used to build the docker conatiner must be used to start the container
>

### 2. Decode directions.txt
When looking inside directions.txt, you can see the text inside is encoded using base64. 
> [!TIP]
> You can run `cat directions.txt` to print out the contents of directions.txt

Run `base64 -d directions.txt ` to decode directions.txt into plain text. You should see 2 things: 
> tomfoolery19
> 
and 
> Your next file is inside a crazy picture
>

> [!Note]
> tomfoolery19 is the password to obtain imbedded files
> - base64 is a utility included in the Linux enviroment. It can be used to decode text from base64 or encode text to base64.
> - The "-d" in the line of text stands for decode, indicating that we want the given file to be decoded
> - Lastly, we include "directions.txt" to indicate the file that contains the text we want to decode

### 3. Find the Picture Named 'crazy.jpg'
a. From inside the workspace directory, run `cd sad`.
> [!Note]
> - `cd` is a built in command within the Linux environment, meaning **c**hange **d**irectory
> - `sad` indicates the directory (aka folder) we want to change to
>

b. Run `ls` to check for the files in the directory. 
> [!Note]
> `ls` is also a built in command within the Linux environment. It stands for list and is used to list all of the visible files and subdirectories within a directory
>

There should be 2 files inside:
> crazy.jpg
>
and
> flag.txt
>
### 4. Optional Step: Check for Hidden Files
> [!TIP]
> Steghide is a steganography tool in Linux. It is used to hide data and/or files within other files, mainly pictures. Because it always requires a password to hide a file within another file, we can use the same password and steghide to check if a file conatins any files hidden with said password.
>

a. Run `steghide info crazy.jpg` to check for hidden files within crazy.jpg
> [!Note]
> - `info` indicates we want show information about the file
> - `crazy.jpg` is the name of the file we want to check
>

b. Enter `y` when prompted, then enter `tomfoolery19` when prompted for the passphrase
> [!Note]
> You may remember `tomfoolery19` from decoding directions.txt earlier. This was the password used to imbed the hidden file into `crazy.jpg`, therefore, when you use this password to uncover hidden files from `crazy.jpg`, you should see information on the imbedded them. In this case, there is only 1 imbedded file named `sha256.txt`.
> 

### 5. Extract the Imbedded file
a. Run steghide extract -sf crazy.jpg  
> [!Note]
> - `extract` indicates we want to retieve hidden data
> - `-sf` means **s**tego **f**ile and signifies there is a file conatining the hidden data
> - `crazy.jpg` is the file that contains the hidden data
>
b. Enter `tomfoolery19` when prompted for a passphrase  
> [!TIP]
> To ensure the file was extracted, run `ls`. You should see the file `sha256.txt` is now in the directory
>

### 6. Find the correct flag
a. Run `cat sha256.txt` to print out all possible flags  
b. Run `echo -n "fullFlag" | sha256sum` to print sha256 hash for each flag, replacing `fullFlag` with each flag. For example, to find the sha256 hash of the first flag, run `echo -n "Flag{youFoundIt}" | sha256sum`
> [!Note]
> `echo` is a Linux tool which prints text to the terminal
> `-n` indicates that we don't want a new line to be created at the end.
> `|` known as pipe, is a built in tool that uses the output of the left side as input for the right side.
> sha256sum is another tool that calculates and prints the sha256 hash of the input
>
c. The sha256 hash of the correct flag is in `flag.txt`. Run `cat flag.txt | grep sha256Hash` to check if the flag is in flag.txt file, replacing `sha256Hash` with the sha256 hash of a flag output from step 6b.
> [!TIP]
> Do steps 6a and 6b for one possible flag then repeat for each possible flag until the correct flag is found
> 

## Correct Flag:
Flag{youPassed} 

