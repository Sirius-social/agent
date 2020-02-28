# Aries RFC 0317: Please ACK Decorator 1.0

- Authors: Igor Fedorov
- Status: [ACCEPTED](/README.md#accepted)
- Since: 2020-28-02
- Status Note:  
- Supersedes: [Indy 0317](https://github.com/hyperledger/aries-rfcs/tree/master/features/0317-please-ack)
- Start Date: 2020-28-02
- Tags: [feature](/tags.md#feature), [decorator](/tags.md#decorator), [test-anomaly](/tags.md#test-anomaly)

## Summary

The PleaseAck Decorator is needed to request the recipient about the delivery status of message.

## Motivation

We need to know if the message has been delivered to the recipient, even if it is crypted.
This decorator is used for this,
when there is such a decorator in the message, we know that we need to send an answer to this message.

## Tutorial




**Protocol**: any

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


**Protocol**: did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/notification/1.0/ack


**message**

- status - PENDING (delivered), OK (readed) 
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

## Reference

The following lists the implementations (if any) of this RFC. Please do a pull request to add your implementation. If the implementation is open source, include a link to the repo or to the implementation within the repo. Please be consistent in the "Name" field so that a mechanical processing of the RFCs can generate a list of all RFCs supported by an Aries implementation.
## Implementations
Name / Link | Implementation Notes
--- | ---
[Indy Cloud Agent - Python](https://github.com/hyperledger/indy-agent/python) | Reference agent implementation contributed by Sovrin Foundation and Community; [MISSING test results](/tags.md#test-anomaly)
[Aries Framework - .NET](https://github.com/hyperledger/aries-framework-dotnet) | .NET framework for building agents of all types; [MISSING test results](/tags.md#test-anomaly)
[Streetcred.id](https://streetcred.id/) | Commercial mobile and web app built using Aries Framework - .NET; [MISSING test results](/tags.md#test-anomaly)
[Aries Cloud Agent - Python](https://github.com/hyperledger/aries-cloudagent-python) | Contributed by the government of British Columbia.; [MISSING test results](/tags.md#test-anomaly)
[Aries Static Agent - Python](https://github.com/hyperledger/aries-staticagent-python) | Useful for cron jobs and other simple, automated use cases.; [MISSING test results](/tags.md#test-anomaly)
[Aries Protocol Test Suite](https://github.com/hyperledger/aries-protocol-test-suite) | ; [MISSING test results](/tags.md#test-anomaly)
