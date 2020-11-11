# GSUTIL is Google Cloud storage CLI
is the command line tool used to manage buckets and objects on Google Storage. 

Basic commands:
List all buckets and files
gsutil ls, gsutil ls -lh gs://bucket-name

Download file	
  gsutil cp gs://bucket-name/dir-path/package-1.1.tgz .

Upload file
  gsutil cp filename gs://bucket-name/directory/

Cat file
  gsutil cat gs://<bucket-name>/<filepath>/

Delete file
  gsutil rm gs://<bucket-name>/<filepath>

Move file
  gsutil mv <src-filepath> gs://<bucket-name>/<directory>/<dest-filepath>

Copy folder
  gsutil cp -r ./conf gs://<bucket-name>/

Show disk usage
  gsutil du -h gs://<bucket-name/<directory>

Create bucket
  gsutil mb gs://<bucket-name>

Caculate file
  sha1sum	gsha1sum syslog-migration-10.0.2.tgz, shasum syslog-migration-10.0.2.tgz

Gsutil help
  gsutil help, gsutil help cp, gsutil help options

# Regional Cloud Storage + Storage Type
gsutil mb -l southamerica-east1 -c nearline gs://bucketname

# Uniform Bucket-Level Access
Desactivate
gsutil mb -b off gs://bucket-with-acls
Activate
gsutil mb -b on gs://bucket-with-no-acls
