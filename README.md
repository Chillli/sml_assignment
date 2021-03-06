# Tutorial for recreating the implementation of “Protocol State Fuzzing of TLS Implementations”

## Download the repository from github

Clone the repository from GitHub by
```
   git clone https://github.com/jderuiter/statelearner
```

## Install TLS implementations
It depends on what kind of implementations you wanna run, the paper tested 9 TLS implementations, here we pick the most common one, OpenSSL as the example. 
We are using MAC for the implementation

### Install OpenSSL

```
sudo apt-get install openssl
```

## Install maven

The repository is managed by using Maven. 
If you already installed maven, ignore this step. 

```
sudo apt-get install maven.
```

## Build the project

```
mvn package shade:shade 
```

## Run TLS implementation

To start a server in our host machine,  go to the examples/openssl/ folder in the cloned repo, and run openssl server with the following command:

```
openssl s_server -key server.key -cert server.crt -CAfile cacert.pem -
```

All required arguments for the server is provided in the current folder, including the key in the "server.key" file, the certificate in the "server.crt" file. 
Then an OpenSSL server is hosted in localhost:4433. You can use "netstat -natp" command to check the condition of your server.

## Run Learner

We advise you to use an IDE to ruan StateLearner.
Then move all files from "statelearner/examples/openssl" to "statelearner/" path.
And declare "server.properties" as the imput argument in your IDE execution configuration. 

The input alphabe for this example is in "server.properties" file:

```
ClientHelloRSA ClientHelloDHE EmptyCertificate ClientKeyExchange ChangeCipherSpec Finished ApplicationData ApplicationDataEmpty Alert10
```

## Result

Learner will create a folder called "ouput_server" and automatically save all results to it. The version of our tested OpenSSL is 1.0.1t. Learner generated two hypothesis of the protocol state machine.
The result is shown in "hypothesis_1.dot.pdf" and "hypothesis_2.dot.pdf" in this repository.


