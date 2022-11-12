# External Communication System

The system that connects all the subcomponents in the laser-tag game together and makes the gameplay possible.

# Spin up the system
The application only works on Ultra96, and thus the instructions below should only be run on the Ultra96.

## Installing Dependencies
```sh
$ pip3 install -r requirements.txt
```

## Creating .env file
A `.env` file should be created at the root of the directory. The file content should be as followed (the value within <> are to be replaced):

```sh
# eval_server
SECRET_KEY=<secret_key_for_eval_server>
EVAL_HOST=<ip_of_eval_server>
EVAL_PORT=<port_of_eval_server>

# MQTT
BROKER_HOST=<mqtt_broker_url>
BROKER_USERNAME=<mqtt_broker_username>
BROKER_PASSWD=<mqtt_broker_password>
# topic that the GAME ENGINE sees
ACTION_TOPIC="action"
GAME_STATE_TOPIC="game_state"
INVALID_TOPIC="invalid"
SUBSCRIBE_TOPIC="grenade"

# data_server
DATA_HOST="0.0.0.0"
DATA_PORT=10000
```

## Running the application
Go into sudo mode for the AI inference to work on FPGA
```sh
$ sudo -i  
```

Then go back to the directory of this repo
```sh
$ cd /path/to/ultra96-external-comm
```

Finally, run the application and specify the player mode (1/2), e.g.,
```sh
$ python3 src/main.py 2  # 2-player mode
```

The application will attempt to connect to evaluation server until it's successfully connected. Similarly, the application also waits for the connection from the relay laptop.