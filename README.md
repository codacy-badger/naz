## naz          

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/ccf655afb3974e9698025cbb65949aa2)](https://www.codacy.com/app/komuw/naz?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=komuw/naz&amp;utm_campaign=Badge_Grade)
[![Build Status](https://travis-ci.com/komuw/naz.svg?branch=master)](https://travis-ci.com/komuw/naz)
[![codecov](https://codecov.io/gh/komuw/naz/branch/master/graph/badge.svg)](https://codecov.io/gh/komuw/naz)


naz is an SMPP client.           
It's name is derived from Kenyan hip hop artiste, Nazizi.                             

> SMPP is a protocol designed for the transfer of short message data between External Short Messaging Entities(ESMEs), Routing Entities(REs) and Short Message Service Center(SMSC). - [Wikipedia](https://en.wikipedia.org/wiki/Short_Message_Peer-to-Peer)

naz currently only supports SMPP version 3.4.

naz is in active development and it's API may change in backward incompatible ways.               
[https://pypi.python.org/pypi/naz](https://pypi.python.org/pypi/naz)

## Installation

```shell
pip install naz
```           


## Usage

#### 1. As a library
```python
import asyncio
import naz


loop = asyncio.get_event_loop()
cli = naz.Client(
    async_loop=loop,
    SMSC_HOST="127.0.0.1",
    SMSC_PORT=2775,
    system_id="smppclient1",
    password="password",
)

# queue messages to send
for i in range(0, 4):
    print("submit_sm round:", i)
    loop.run_until_complete(
        cli.submit_sm(
            msg="Hello World-{0}".format(str(i)),
            correlation_id="myid12345",
            source_addr="254722111111",
            destination_addr="254722999999",
        )
    )

# connect to the SMSC host
reader, writer = loop.run_until_complete(cli.connect())
# bind to SMSC as a tranceiver
loop.run_until_complete(cli.tranceiver_bind())

# read any data from SMSC, send any queued messages to SMSC and continually check the state of the SMSC
gathering = asyncio.gather(cli.send_forever(), cli.receive_data(), cli.enquire_link())
loop.run_until_complete(gathering)

loop.run_forever()
loop.close()
```


#### 2. As a cli app
naz also ships with a commandline interface app called `naz-cli`.            
run:                
```shell
naz-cli ....
```              

To see help:
```shell
naz-cli --help                 
```



## Features
- 
- 
- Well written(if I have to say so myself):
  - [Good test coverage](https://codecov.io/gh/komuw/naz)
  - [Passing continous integration](https://circleci.com/gh/komuw/naz)
  - [High grade statically analyzed code](https://www.codacy.com/app/komuw/naz/dashboard)


## Development setup
- fork this repo.
- you need to have python3 installed, this project is python3 only.
- cd naz
- sudo apt-get install pandoc
- open an issue on this repo. In your issue, outline what it is you want to add and why.
- install pre-requiste software:             
```shell
apt-get -y install pandoc && pip install -e .[dev,test]
```                   
- make the changes you want on your fork.
- your changes should have backward compatibility in mind unless it is impossible to do so.
- add your name and contact(optional) to CONTRIBUTORS.md
- add tests
- format your code using [black](https://github.com/ambv/black):                      
```shell
black --line-length=100 --py36 .
```                      
- run [flake8](https://pypi.python.org/pypi/flake8) on the code and fix any issues:                      
```shell
flake8 .
```                      
- run [pylint](https://pypi.python.org/pypi/pylint) on the code and fix any issues:                      
```shell
pylint --enable=E --disable=W,R,C --unsafe-load-any-extension=y naz/
```    
- run tests and make sure everything is passing:
```shell
make test
```
- open a pull request on this repo.               
NB: I make no commitment of accepting your pull requests.                 



## TODO
- 

