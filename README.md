[README (1).md](https://github.com/user-attachments/files/29076287/README.1.md)<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Eric Hayes  
**Email:** 93eriich@gmail.com

---



---

## Introducing Today's Project!

In this project, I will demonstrate using encryption to secure data. The goal is to create encryption keys with AWS KMS (Key Management System), encrypt a DynamoDB table's data with that key, then test access using IAM users. 

### Tools and concepts

Services I used include AWS KMS (Key Management Service), DynamoDB, and AWS IAM. Key concepts I learnt include encryption, database tables, and KMS using permission to actions rather than access to the key itself; Creating a user to test access. 

### Project reflection

This project took me approximately 1.5 hours including demo time. The most challenging part was understanding how encryption works differently from other access control tool. It was most rewarding to see our test user gain access to encryption.

I chose to do this project today to learn all about encryption, securing data, and how it works. 

---

## Encryption and KMS

Encryption is the process of turning original/plaintext data into a secure format. Companies and developers do this to secure their data from unauthorized users. Encryption keys are secure code that informs an algorithm how it should encrypt. 

AWS KMS is a vault for my encryption keys. Key management systems are important because they help us secure and manage the keys we use to encrypt data. Unauthorized access to the key + exposing our encrypted data, which puts security at risk. 

Encryption keys are broadly categorized as symmetric and asymmetric. I set up a symmetric key because we'll be using the same key to encrypt and decrypt the data. Asymmetric keys would be a good choice if we need different keys for encryption and decryption

![Image](http://learn.nextwork.org/encouraged_silver_clever_sea_lion/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is a fast and flexible database service. DynamoDB is great for applications that need fast access to large amounts of data, e.g., gaming

The different encryption options in DynamoDB include DynamoDB-owned, AWS-managed key, and customer-managed. Their differences are based on who manages the key and whether we have visibility. I selected the CMK to use our created KMS key.

![Image](http://learn.nextwork.org/encouraged_silver_clever_sea_lion/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Rather than controlling who has access to the key, KMS manages user permissions by controlling the actions that people can do with that key. In our case, even if we permitted our test user to see the key, it would need permission to decrypt.

Despite encrypting my DynamoDB table, I could still see the table's items because we are users of the key... DynamoDB uses transparent data encryption, which means it does the encryption and decryption process for us, since it knows we're authorized.

![Image](http://learn.nextwork.org/encouraged_silver_clever_sea_lion/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user to validate whether an unauthorized user can still access encrypted data. The permission policies granted to this user are DynamoDB full access, but NOT En/Decryption permission with AWS KMS. 

After accessing the DynamoDB table as the test user, I encountered an "access denied" message because our test user has no access to decryption with the key. This confirmed that the encryption key can be used to secure data 

![Image](http://learn.nextwork.org/encouraged_silver_clever_sea_lion/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I made it a key user in the KMS console. My key's policy was updated to allow network-kms-user to encrypt, decrypt, reencrypt, etc., using the key

Using the test user, I retried accessing the Dynamo DB table. I observed that the user can see the data inside again, which confirmed that making it a key user is an effective way to authorize someone to see encrypted data. 

Encryption secures data instead of an entire resource or service. I could combine encryption with other access control tools like security groups and permission policies to have two layers of security: the resource level and then the data level.

![Image](http://learn.nextwork.org/encouraged_silver_clever_sea_lion/uploads/aws-security-kms_feffb2fb8)

---

---

