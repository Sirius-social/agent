# Aries RFC 0317: Please ACK Decorator 1.0

- Authors: [Igor Fedorov](https://github.com/igorexax3mal), [Pavel Minenkov](https://github.com/Purik)
- Since: 2020-28-02
- Inherited from: [Aries 0015](https://github.com/hyperledger/aries-rfcs/tree/master/features/0015-acks), [Aries 0019](https://github.com/hyperledger/aries-rfcs/tree/master/features/0019-encryption-envelope)
- Start Date: 2020-28-02


## Summary

The PleaseAck Decorator is needed to request the recipient about the delivery status of message.

## Motivation

We need to know if the message has been delivered to the recipient, even if it is encrypted.
This decorator is used for this,
when there is such a decorator in the message, we know that we need to send an answer to this message.

## Tutorial

**message**

- message_id - "@id" of message to be  
- serviceEndpoint - endpoint for send a response  .


Example:

```json
{
    "@id": "123456780",
    "@type": "did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/.../.../...",
    "~please_ack": { "message_id": "id",
                    "serviceEndpoint" : "https://..."
                    }
}
```

when message with decorator  "~please_ack" arrived , send message  to endpoint in "serviceEndpoint" with "PENDING" status:


**Protocol**: `did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/notification/1.0/ack`


**message**

- status - `PENDING` (delivered), `OK` (readed) 
- serviceEndpoint - endpoint URL for send a response  .

Example:

```json
{
        "@type": "did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/notification/1.0/ack",
            "@id": "06d474e0-20d3-4cbf-bea6-6ba7e1891240",
            "status": "PENDING",
            "~thread": {
                       "thid": "message_id"
                        }
  }
 ```
