# Sirius media and file exchanging Protocol 1.0

- Authors: [Igor Fedorov](https://github.com/igorexax3mal)
- Since: 2020-02-01 
- Inherited from: [Aries 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)
- Start Date: 2019-01-16
- Tags: [feature](/tags.md#feature), [protocol](/tags.md#protocol), [test-anomaly](/tags.md#test-anomaly)

## Summary

The media and file exchanging protocol describes a stateless, easy to support user content exchange  protocol. It has a single multiple message types used to transmit files and media.

## Motivation

It is a useful feature to be able to transmit encrypted content in [P2P](https://github.com/hyperledger/aries-rfcs/tree/master/features/0160-connection-protocol "P2P") context. Any media content is encrypted by key, decrypted key is presented in message, so sender can control participiants who can get access to semantic of the files located on CDN.

## Tutorial

#### Roles

There are two roles in this protocol: **sender** and **receiver**. It is anticipated that both roles are supported by agents that provide an interface for humans, but it is possible for an agent to only act as a sender (do not process received messages) or a receiver (will never send messages).

#### States

There are not really states in this protocol, as sending a message leaves both parties in the same state they were before.

#### Out of Scope

There are many useful features of user messaging systems that we will not be adding to this protocol. We anticipate the development of more advanced and full-featured message protocols to fill these needs. Features that are considered out of scope for this protocol include:

- message replies (threading)
- multi-party (group) messages

## Reference

**Protocol**: did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/

**message**

- sent_time - timestamp in ISO 8601 UTC
- content - content of the user intended message as a string.
- The `~l10n` block SHOULD be used, but only the `locale` presented.

Example:

```json
{
    "@id": "123456780",
    "@type": "did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/message",
    "~l10n": { "locale": "en" },
    "sent_time": "2019-01-15 18:42:01Z",
    "content": "Your hovercraft is full of eels."
}
```


## Attachments

**Protocol**: did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/image  - Image (.jpg, .png etc.)

**Protocol**: did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/video  - Video (.mp4 etc.)

**Protocol**: did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/audio  - Audio (.wav, .mp3 etc.)

**Protocol**: did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/doc    - Other type 


## Tutorial For Attachnmetns
To add attachments in message :

1. Choose  desired type of attachment
2. Encrypt file 
3. add type of attachment and DecryptionKey to message

**message**

- preview_url - (optional) thumbnail preview if need
- url - URL to download encrypted file
- content_type -  type of attachment(one of image, video, audio ,doc)
- decryption_key - your Decryption Key in BASE64 format

Example:

```json
{
    "@id": "123456780",
    "@type": "did:sov:BzCbsNYhMrjHiqZDTUASHg;spec/basicmessage/1.0/image",
    "~l10n": { "locale": "en" },
    "sent_time": "2019-01-15 18:42:01Z",
    "url": "https://....",
    "preview_url": "https://....",
    "content_type": "image",
    "decryption_key": "<BASE64>Decryption Key",
}
```
## Anvanced questions
- Receive receipts

## Unresolved questions

- Receive receipts (NOT read receipts) may be implicitly supported by an ack decorator with pre-processing support.
