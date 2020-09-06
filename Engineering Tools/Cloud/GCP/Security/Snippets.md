# Snippets

```bash
# Create a key
openssl rand 32 > mykey.txt
# Verify key
more mykey.txt

# Download Google CE public certificate
curl \ https://cloud-certs.storage.googleapis.com/google-cloud-csek-ingress.pem \ > gce-cert.pem
# Extract public key from the certificate
openssl x509 -pubkey -noout -in gce-cert.pem > pubkey.pem
# RSA-wrap the custom key 
openssl rsautl -oaep -encrypt -pubin -inkey pubkey.pem -in \ mykey.txt -out rsawrappedkey.txt
# Encode the RSA-wrapped key in base64
openssl enc -base64 -in rsawrappedkey.txt | tr -d '\n' | sed -e \ '$a\' > rsawrapencodedkey.txt
# View the RSA-wrapped key
cat rsawrapencodedkey.txt

# Format and mount the encrypted volume
sudo mkfs.ext4 /dev/disk/by-id/google-encrypted-disk-1 mkdir encrypted sudo mount /dev/disk/by-id/google-encrypted-disk-1 encrypted/
```
**Using custom keys for encryption**
```bash
# Enable cloudkms
> gcloud services enable cloudkms.googleapis.com
# Setup the name of key objects
> KEYRING_NAME=lab-keyring
> CRYPTOKEY_1_NAME=labkey-1
> CRYPTOKEY_2_NAME=labkey-2
# Create keyring
gcloud kms keyrings create $KEYRING_NAME --location us
# Create keys
gcloud kms keys create $CRYPTOKEY_1_NAME --location us \ --keyring $KEYRING_NAME --purpose encryption
gcloud kms keys create $CRYPTOKEY_2_NAME --location us \ --keyring $KEYRING_NAME --purpose encryption
# Obtain default encryption key information from a bucket
gsutil kms encryption gs://$DEVSHELL_PROJECT_ID-kms
# Assign Cloud KMS keys to a service account
# comand format is: gsutil kms authorize -p [PROJECT_STORING_OBJECTS] -k [KEY_RESOURCE]
gsutil kms authorize -p $DEVSHELL_PROJECT_ID -k \ projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME gsutil kms authorize -p $DEVSHELL_PROJECT_ID -k \ projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_2_NAME
# set default key for a bucket 
gsutil kms encryption -k \ projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME \ gs://$DEVSHELL_PROJECT_ID-kms

# encrypt individual objects
gsutil -o \ "GSUtil:encryption_key=projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_2_NAME" \ cp file3.txt gs://$DEVSHELL_PROJECT_ID-kms
# Identify the key used to encrypt an object
gsutil ls -L gs://$DEVSHELL_PROJECT_ID-kms/file3.txt
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUyMDI2NDUzNl19
-->