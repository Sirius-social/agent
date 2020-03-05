# Sirius extension for Aries RFC 0317: please ACK decorator

- Authors: [Igor Fedorov](https://github.com/igorexax3mal), [Pavel Minenkov](https://github.com/Purik)
- Since: 2020-28-02
- Inherited from: [Aries 0015](https://github.com/hyperledger/aries-rfcs/tree/master/features/0015-acks), [Aries 0019](https://github.com/hyperledger/aries-rfcs/tree/master/features/0019-encryption-envelope)
- Start Date: 2020-28-02


## Summary

The PleaseAck Decorator is needed to notify sender about the delivery status of message without [unpacking](https://github.com/hyperledger/aries-rfcs/tree/master/features/0019-encryption-envelope#authcrypt-mode-vs-anoncrypt-mode) message via **wallet** calls.

## Motivation

Independently of [encryption mode](https://github.com/hyperledger/aries-rfcs/tree/master/features/0019-encryption-envelope#authcrypt-mode-vs-anoncrypt-mode), sometimes it is good for interactivity in Connector App to notify sender about message was delivered to recepient device but the wallet owner has not read it yet. Application on recepient side can not inject [please_ack](https://github.com/hyperledger/aries-rfcs/tree/master/features) decorator to message before encryption cause of application on sender side should not store wallet **pass_phrase** for security best practices. Sirius Communicator inject **please_ack** decorator to [packet](https://github.com/hyperledger/aries-rfcs/tree/master/features/0019-encryption-envelope#pack_message-return-value-authcrypt-mode) buffer before sending wired data to Endpoint.

## Tutorial

**message**

- message_id - "@id" of message to be  
- serviceEndpoint - endpoint for send a response  .


Example for Authcrypt mode:

```json
{
    "protected": "eyJlbmMiOiJ4Y2hhY2hhMjBwb2x5MTMwNV9pZXRmIiwidHlwIjoiSldNLzEuMCIsImFsZyI6IkF1dGhjcnlwdCIsInJlY2lwaWVudHMiOlt7ImVuY3J5cHRlZF9rZXkiOiJMNVhEaEgxNVBtX3ZIeFNlcmFZOGVPVEc2UmZjRTJOUTNFVGVWQy03RWlEWnl6cFJKZDhGVzBhNnFlNEpmdUF6IiwiaGVhZGVyIjp7ImtpZCI6IkdKMVN6b1d6YXZRWWZOTDlYa2FKZHJRZWpmenRONFhxZHNpVjRjdDNMWEtMIiwiaXYiOiJhOEltaW5zdFhIaTU0X0otSmU1SVdsT2NOZ1N3RDlUQiIsInNlbmRlciI6ImZ0aW13aWlZUkc3clJRYlhnSjEzQzVhVEVRSXJzV0RJX2JzeERxaVdiVGxWU0tQbXc2NDE4dnozSG1NbGVsTThBdVNpS2xhTENtUkRJNHNERlNnWkljQVZYbzEzNFY4bzhsRm9WMUJkREk3ZmRLT1p6ckticUNpeEtKaz0ifX0seyJlbmNyeXB0ZWRfa2V5IjoiZUFNaUQ2R0RtT3R6UkVoSS1UVjA1X1JoaXBweThqd09BdTVELTJJZFZPSmdJOC1ON1FOU3VsWXlDb1dpRTE2WSIsImhlYWRlciI6eyJraWQiOiJIS1RBaVlNOGNFMmtLQzlLYU5NWkxZajRHUzh1V0NZTUJ4UDJpMVk5Mnp1bSIsIml2IjoiRDR0TnRIZDJyczY1RUdfQTRHQi1vMC05QmdMeERNZkgiLCJzZW5kZXIiOiJzSjdwaXU0VUR1TF9vMnBYYi1KX0pBcHhzYUZyeGlUbWdwWmpsdFdqWUZUVWlyNGI4TVdtRGR0enAwT25UZUhMSzltRnJoSDRHVkExd1Z0bm9rVUtvZ0NkTldIc2NhclFzY1FDUlBaREtyVzZib2Z0d0g4X0VZR1RMMFE9In19XX0=",
    "iv": "ZqOrBZiA-RdFMhy2",
    "ciphertext": "K7KxkeYGtQpbi-gNuLObS8w724mIDP7IyGV_aN5AscnGumFd-SvBhW2WRIcOyHQmYa-wJX0MSGOJgc8FYw5UOQgtPAIMbSwVgq-8rF2hIniZMgdQBKxT_jGZS06kSHDy9UEYcDOswtoLgLp8YPU7HmScKHSpwYY3vPZQzgSS_n7Oa3o_jYiRKZF0Gemamue0e2iJ9xQIOPodsxLXxkPrvvdEIM0fJFrpbeuiKpMk",
    "tag": "kAuPl8mwb0FFVyip1omEhQ==",
    "~please_ack": { 
	"message_id": "id",
        "serviceEndpoint" : "https://..."
    }
}
```

when wired message with decorator  "~please_ack" arrived , send message  to endpoint in "serviceEndpoint" with "PENDING" status:


**Protocol**: `did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/notification/1.0/ack`


**message**

- status - `PENDING` (delivered), `OK` (readed) 
- serviceEndpoint - endpoint URL for send a response  .
