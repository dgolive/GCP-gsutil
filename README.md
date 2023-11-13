# GSUTIL - Google Cloud Storage CLI
gsutl is the command line tool used to manage buckets and objects on Google Storage.

####
- [Cloud Storage operations]()
- [Access Control](#access-control) 
- [Versioning](#versioning)
- [Signing URLs](#signing-urls)
- [Backup](#backup)
- [Lifecycle](#lifecycle)

### Cloud Storage operations
***Create a bucket***
```
gsutil mb gs://bucket-name
```

***Creating a regional cloud storage + storage Type***
```
gsutil mb -l southamerica-east1 -c nearline gs://bucketname
```

***List all buckets***
```
gsutil ls
```

***List all buckets and files***
```
gsutil ls -lh gs://bucket-name 
```

***Get information about the file***
```
gsutil ls -L gs://bucket-name/testfile.txt 
```

***Copy file (download)***
```
gsutil cp gs://bucket-name/dir-path/package-1.1.tgz .
```

***Copy file (upload)***
```
gsutil cp filename gs://bucket-name/directory/
```

***Cat file***
```
gsutil cat gs://bucket-name/filepath/
```

***Delete file***
```
gsutil rm gs://bucket-name/filepath
```

***Move file***
```
gsutil mv src-filepath gs://bucket-name/directory/dest-filepath
```

***Copy folder***
```
gsutil cp -r ./conf gs://bucket-name/
```

***Show disk usage***
```
gsutil du -h gs://bucket-name/directory
```

***Calculate file***
```
sha1sum	gsha1sum syslog-migration-10.0.2.tgz, shasum syslog-migration-10.0.2.tgz
```

***Gsutil help***
```
gsutil help, gsutil help cp or gsutil cp help, gsutil help options
```
<br />

### Access control

***Make the file public***
```
 gsutil acl ch -u allUsers:r gs://whizlabs-bucket/file.pdf
```

***Uniform Bucket-Level Access - Enabling***
```
gsutil mb -b on gs://bucket-with-no-acls
```

***Uniform Bucket-Level Access - Disabling***
```
gsutil mb -b off gs://bucket-with-acls
```
<br />

### Versioning
***Bucket versioning - Enabling***
```
gsutil versioning set on gs://bucketname
```

***Bucket versioning - Disabling***
```
gsutil versioning set off gs://bucketname
```
<br />

### Signed URLs
***Signed URLs*** 
```
gsutil signurl -d 10m -m GET /ath/private_key.json  gs://bucketname/filename
```

***Signed URLs access for 10 minutes***
```
gsutil signurl -d 10m -m GET /path/private_key.json gs://bucketname>/img/*.png*
```
<br />

### Backup
***rsync - automatic backup***
```
gsutil rsync source folder target folder
```

***rsync - local folder with storage bucket***
```
gsutil -m rsync -r -d ./myfolder gs://bucketname
```

If you don’t want to have to run the gsutil command every time you make a change in the source folder, you can set up a cron job on your local with crontab -e or the equivalent for windows machines. For instance the following cron job will backup your local folder to Google Cloud every 15mn.
\*/15  * * * * gsutil -m rsync -r -d /full path to myfolder/ gs://mybucket >> /full path to log file

<br />

### Lifecycle
***Lifecycle using json file***
```
gsutil lifecycle set config_file.json gs://bucket_name
```

The following lifecycle management configuration JSON document specifies that all objects in this bucket that are more than 365 days old are deleted automatically (config_file.json):

```   
   {
      "rule":
      [
        {
          "action": {"type": "Delete"},
           "condition": {"age": 365}
        }
      ]
    }
```
