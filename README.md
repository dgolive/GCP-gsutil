# GSUTIL is Google Cloud storage CLI
is the command line tool used to manage buckets and objects on Google Storage. 

Basic commands:
List all buckets and files
gsutil ls, gsutil ls -lh gs://bucket-name

***Copy file (download)*** ~$ gsutil cp gs://bucket-name/dir-path/package-1.1.tgz .

***Copy file (upload)*** ~$ gsutil cp filename gs://bucket-name/directory/

***Cat file*** ~$  gsutil cat gs://<bucket-name>/<filepath>/

***Delete file*** ~$ gsutil rm gs://<bucket-name>/<filepath>

***Move file*** ~$ gsutil mv <src-filepath> gs://<bucket-name>/<directory>/<dest-filepath>

***Copy folder*** ~$ gsutil cp -r ./conf gs://<bucket-name>/

***Show disk usage*** ~$ gsutil du -h gs://<bucket-name/<directory>

***Create bucket*** ~$ gsutil mb gs://<bucket-name>

***Caculate file*** ~$ sha1sum	gsha1sum syslog-migration-10.0.2.tgz, shasum syslog-migration-10.0.2.tgz

***Gsutil help*** ~$ gsutil help, gsutil help cp, gsutil help options


**Regional Cloud Storage + Storage Type** 
gsutil mb -l southamerica-east1 -c nearline gs://bucketname

**Uniform Bucket-Level Access**
Enabling
  $ gsutil mb -b on gs://bucket-with-no-acls
Disabling 
  $ gsutil mb -b off gs://bucket-with-acls

**Bucket versioning**
Enabling
  $ gsutil versioning set on gs://bucketname
Disabling
  $ gsutil versioning set off gs://bucketname

When versioning is enabled on a bucket, objects become accessible by specifying their version number. Listing the content of a bucket will show the version numbers of its objects as such:
gs://bucketname/filename#version_number_1
gs://bucketname/filename#version_number_2
...
To retrieve the correct version, simply append the version number to the object name in the cp command.
The object versioning page offers more details on the subject.


**Signed URLs**
Signed URLs is a mechanism for query string authentication for buckets and objects. In other words, Signed urls provide a way to give time-limited read or write access to anyone in possession of the URL, regardless of whether they have a Google account. To create a signed url you first need to generate a generate a private key following these instructions. Click on Create a service account key, select your project, and download the JSON file that contains your private key.
You can now create a signed urls for one of your file with
$ gsutil signurl -d 10m -m GET <path/private_key.json>  gs://<bucketname>/<filename>
Note that signed urls do not work on directories. If you want to give access to multiple files you can use wildcards. For instance the following command will give access for 10 minutes on all the png files in the gs://<bucketname>/img/ folder.
$ gsutil signurl -d 10m -m GET <path/private_key.json> gs://<bucketname>/img/*.png*
Check the signed urls page for more info

**rsync**
to create an automatic backup of your data in the cloud. The rsync command follows:
$ gsutil rsync <source folder> <target folder>

Consider a local folder ./myfolder and the <bucketname> bucket, the following command synchronizes the content of the local folder with the storage bucket:

$ gsutil -m rsync -r -d ./myfolder gs://<bucketname>
The content of gs://<bucketname> will match the content of your local ./myfolder directory, effectively backing up the local documents.
Note the presence of the -r flag which ensures that all subfolders are matched.
The -d flag is to be used with caution as it will delete the content in the target when deleted from the source. If you inadvertently make a mistake in your command, for instance inverting the source and target folders, you may end up deleting your content. A good way to ensure that does not happen is to enable bucket versioning.
If you don’t want to have to run the gsutil command every time you make a change in the source folder, you can set up a cron job on your local with crontab -e or the equivalent for windows machines. For instance the following cron job will backup your local folder to Google Cloud every 15mn.
\*/15  * * * * gsutil -m rsync -r -d < full path to myfolder> gs://mybucket >> <full path to log file>


**Service accounts**
Service accounts are special accounts that represent software rather than people. They are the most common way applications authenticate with Google Cloud Storage. Every project has service accounts associated with it, which may be used for different authentication scenarios, as well as to enable advanced features such as Signed URLs and browser uploads using POST.
When you use a service account to authenticate your application, you do not need a user to authenticate to get an access token. Instead, you obtain a private key from the Google Cloud Platform Console, which you then use to send a signed request for an access token. You can then use the access token like you normally would. For more information see the Google Cloud Platform

**Lifecycle**
To enable lifecycle for a bucket with settings defined in the config_file.json file, run:
$ gsutil lifecycle set <config_file.json> gs://<bucket_name>

