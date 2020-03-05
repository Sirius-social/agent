# Sirius media and file exchanging Protocol 1.0

- Authors: [Igor Fedorov](https://github.com/igorexax3mal), [Pavel Minenkov](https://github.com/Purik)
- Since: 2020-02-01 
- Inherited from: [Aries 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)
- Start Date: 2019-01-16


## Summary

The media and file exchanging protocol describes a stateless, easy to support user content exchange  protocol. It has multiple message types used to transmit files and media.

## Motivation

It is a useful feature to be able to transmit encrypted content in [P2P](https://github.com/hyperledger/aries-rfcs/tree/master/features/0160-connection-protocol) context. Any media content is encrypted by key, decrypted key is presented in message, so sender can control participiants who can get access to semantic of the files located on CDN.

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

**Protocol**: `https://github.com/Sirius-social/agent/tree/master/messages/cdn/1.0/`

**message**

- sent_time - timestamp in ISO 8601 UTC
- content - content of the user intended message as a string.
- The `~l10n` block SHOULD be used, but only the `locale` presented.

Example:

```json
{
  "@type": "https://github.com/Sirius-social/agent/tree/master/messages/cdn/1.0/image",
  "@id": "iM95e-b6173702-8b56-461c-ac56-84a8fee08aac",
  "url": "https://socialsirius.com/content/public/xxx.jpg",
  "preview_url": "null",
  "sent_time": "2020-03-05 14:56:04+0300",
  "decryption_key": "HRjNKAl6gbemiUuHeaEjEA==\n",
  "~l10n": {
    "locale": "en"
  },
  "content_type": "image"
}
```


## Message types

**type**: `https://github.com/Sirius-social/agent/tree/master/messages/cdn/1.0/image`  - Image (`.jpg`, `.png` etc.)

**type**: `https://github.com/Sirius-social/agent/tree/master/messages/cdn/1.0/video`  - Video (`.mp4` etc.)

**type**: `https://github.com/Sirius-social/agent/tree/master/messages/cdn/1.0/audio`  - Audio (`.wav`, `.mp3` etc.)

**type**: `https://github.com/Sirius-social/agent/tree/master/messages/cdn/1.0/doc`    - Other type 


## Tutorial For message constructing

To build message :

1. Choose  desired type of attachment
2. Encrypt file 
3. Upload file to preferred CDN provider with public access to file
3. Add type of attachment and DecryptionKey to message

**message**

- preview_url - (optional) thumbnail preview if need
- url - URL to download encrypted file
- content_type -  type of attachment(one of image, video, audio ,doc)
- decryption_key - your Decryption Key in BASE64 format

## Anvanced questions

### Receive receipts
To mark message as received or achnowleged, refer to [sirius ack concept](https://github.com/Sirius-social/agent/blob/master/messages/PleaseAckDecorator.md)
