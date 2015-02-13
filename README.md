s3upload
========

Overview
--------

s3transmit is a multi-threaded multi-part capable uploader for Amazon S3.
It's goal is to be speedy and reliable.

The multi-part upload is done for larger files using multiple threads to
improve performance.  A single thread tends to get bogged down in the upload,
where multiple threads can saturate our 20Mbps.  For smaller files, this
s3transmit will upload many of them in parallel for similar reasons.

It first transfers the small files and then works on the large.

Usage
-----

The command-line usage is:

    export AWS_ACCESS_ID=My_AWS_ID
    export AWS_SECRET_KEY=My_AWS_Secret
    s3transfer <source dir> <bucket/prefix>

It uploads everything from the source directory to the specified bucket.  If
the bucket has "/path" in it, the files are placed in the "folder" in S3
specified by "/path" under that bucket.  For example:

    s3transfer uploads/ backup/uploaded

Will upload files from the "uploads" directory into the "backup" bucket with
in the "uploaded" folder.

"large" files are defined as those more than 40MiB.  This is currently
hard-coded in the code.  Large files are uploaded using multi-part upload.

8 upload threads are used (hard-coded currently).
