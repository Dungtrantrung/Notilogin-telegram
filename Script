#!/bin/bash
# ID chat Telegram
USERID="Your-User-ID"

# API Token bot
TOKEN="Your-Token_ID"

TIMEOUT="10"

URL="https://api.telegram.org/bot$TOKEN/sendMessage"

DATE_EXEC="$(date "+%d %b %Y %H:%M")"
TMPFILE='/tmp/ipinfo.txt'

if [ -n "$SSH_CLIENT" ]; then
    IP=$(echo $SSH_CLIENT | awk '{print $1}')
    PORT=$(echo $SSH_CLIENT | awk '{print $3}')
    HOSTNAME=$(hostname -f)
    IPADDR=$(echo $SSH_CONNECTION | awk '{print $3}')

    curl http://ipinfo.io/$IP -s -o $TMPFILE
    CITY=$(cat $TMPFILE | jq '.city' | sed 's/"//g')
    REGION=$(cat $TMPFILE | jq '.region' | sed 's/"//g')
    COUNTRY=$(cat $TMPFILE | jq '.country' | sed 's/"//g')
    ORG=$(cat $TMPFILE | jq '.org' | sed 's/"//g')

    TEXT=$(echo -e "SSH login warning \n \nServer: $HOSTNAME \n \nSend Time: $DATE_EXEC \n \nUser Login: ${USER} logged in to $HOSTNAME/$IPADDR \n \nLogin IP: $IP")

    curl -s -X POST --max-time $TIMEOUT $URL -d "chat_id=$USERID" -d text="$TEXT" > /dev/null

    rm -rf $TMPFILE
fi
