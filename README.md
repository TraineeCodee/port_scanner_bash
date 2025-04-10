
#!/bin/bash

# Simple Port Scanner using netcat (nc)

# Check if target is provided
if [ -z "$1" ]; then
    echo "Usage: $0 <target> [start_port] [end_port]"
    exit 1
fi

TARGET=$1
START_PORT=${2:-1}
END_PORT=${3:-1024}

echo "Scanning $TARGET from port $START_PORT to $END_PORT..."

for ((port=START_PORT; port<=END_PORT; port++))
do
    nc -z -v -w1 $TARGET $port 2>&1 | grep -q succeeded && echo "Port $port is OPEN"
done
