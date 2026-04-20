The Nautilus DevOps team is focusing on improving their data security by using AWS KMS. 
Your task is to create a KMS key and manage the encryption and decryption of a pre-existing sensitive file using the KMS key.

Specific Requirements:

1. Create a symmetric KMS key named nautilus-KMS-Key to manage encryption and decryption.
2. Encrypt the provided SensitiveData.txt file (located in /root/), base64 encode the ciphertext,
and save the encrypted version as EncryptedData.bin in the /root/ directory.
3. Try to decrypt the same and verify that the decrypted data matches the original file.
Make sure that the KMS key is correctly configured. The validation script will test your 
configuration by decrypting the EncryptedData.bin file using the KMS key you created.



<img width="1512" height="477" alt="image" src="https://github.com/user-attachments/assets/7d4168ac-3929-41b8-a370-188325a6c8f4" />


<img width="1474" height="398" alt="image" src="https://github.com/user-attachments/assets/cbc62595-9861-49b3-8923-99b44599bc89" />



```
aws kms encrypt \
    --key-id alias/nautilus-KMS-Key \
    --plaintext fileb://SensitiveData.txt \
    --output text \
    --query CiphertextBlob | base64 --decode > /root/EncryptedData.bin
```

<img width="451" height="199" alt="image" src="https://github.com/user-attachments/assets/3c4ffb34-dd46-41c2-a772-215b892fa027" />




```
aws kms decrypt \
    --ciphertext-blob fileb://EncryptedData.bin \
    --output text \
    --query Plaintext | base64 --decode > decrypted_file.txt
```

<img width="607" height="169" alt="image" src="https://github.com/user-attachments/assets/f2c99148-a0e9-4bf5-bd25-8ec3184c44b5" />


you will see the same mmesage of the original `SensitiveData.txt` file **This is a sensitive file**
