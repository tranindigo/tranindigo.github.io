---
title: "An introduction to AWS KMS: Envelope Encryption"
date: "2020-08-25"
categories: 
  - "aws"
  - "devops"
tags: 
  - "cloudtrail"
  - "encryption"
  - "keys"
  - "kms"
---

AWS Key Management Service (KMS) is a fully-managed service allows you to create and manage cryptographic keys and control their use across a wide range of AWS services. This is useful because it allows you to centrally manage the encryption keys that control access to your data.

#### Features

KMS is durable to make sure that your keys are never lost. KMS stores multiple copies of encrypted versions of your keys in systems that are designed for 99.999999999% durability. KMS is also designed to be a highly available service by using a redundant architect that spans multiple Availability Zones in each region. However, KMS keys are region-specific, which means that once they are created, keys cannot be transferred to another AWS region. KMS also allows you to rotate your keys, a process that creates a new backing key to perform encryption and decryption. You can configure AWS to automatically rotate keys yearly. AWS CloudTrail can also integrate with KMS to log and audit key use. Logs are delivered to a specified S3 bucket.

#### Asymmetric vs Symmetric encryption

KMS allows you to create keys for both symmetric and asymmetric encryption. Symmetric encryption uses the same secret key to perform the encryption and decryption process. On the other hand, asymmetric encryption (also known as public-key encryption), uses two keys. The public key is used for encryption while a matching private key is used for decryption.

KMS starts with the creation of a Customer Master Key (CMK). AWS KMS uses envelope encryption to protect your data with its services and client-side tool-kits. Envelope encryption works as follows:

1. AWS KMS generates a data key that is used to encrypt data locally in the AWS service or in your app.
2. The data key is then encrypted under a CMK of your choosing (hence the name "envelope" encryption).
3. AWS services encrypt your data and store an encrypted copy of the data key along with the encrypted data.
4. When a service needs to decrypt your data it requests KMS to decrypt the data key using your CMK. If the user is authorized to decrypt under your CMK, the AWS service will receive the decrypted data key from AWS KMS.
5. The AWS service then decrypts your data and returns it in plaintext.
6. Note that a decrypted data key is needed to decrypt your data.
