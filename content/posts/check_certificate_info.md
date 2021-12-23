---
title: "Ho to check certificate information"
date: 2021-12-23T12:28:45+01:00
draft: false
---

It comes handy to check certificate dates and some useful info. I've created a script that prints out those info in a simple way:

```bash
#!/bin/bash

readonly SERVERNAME="$1"
readonly DEFAULT_PORT="443"
USER_DEFINED_PORT="${2}"
readonly PORT="${USER_DEFINED_PORT:=$DEFAULT_PORT}"

if [ -z "$SERVERNAME" ]
  then
    echo "You have to specify a servername"
    exit 1
fi

echo "Checking \"$SERVERNAME\" on port \"$PORT\""
echo "========== DATES =========="
echo | openssl s_client -servername "$SERVERNAME" -connect "$SERVERNAME":"$PORT" 2>/dev/null | openssl x509 -noout -dates

echo "========== ISSUER / ISSUED TO =========="
echo | openssl s_client -servername "$SERVERNAME" -connect "$SERVERNAME":"$PORT" 2>/dev/null | openssl x509 -noout -issuer -subject

echo "========== FINGERPRINT =========="
echo | openssl s_client -servername "$SERVERNAME" -connect "$SERVERNAME":"$PORT" 2>/dev/null | openssl x509 -noout -fingerprint
```

