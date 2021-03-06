iiESI
=====

iiESI.org website

## Requirements
Git  
AWS CLI (https://github.com/aws/aws-cli)

## Steps to push files to test and prod
1) Make sure your files are up to date.

```
/Volumes/websites/iiesidev
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
```

2) Make your changes on dev and push them to GHE.
```
/Volumes/websites/iiesidev
$ git commit -a -m 'Added new cool widget to home page.'
...
$ git push
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 2.96 MiB | 1.03 MiB/s, done.
Total 5 (delta 3), reused 0 (delta 0)
To https://github.nrel.gov/communications/iiesi.git
   76fe0be..fa268f9  master -> master
```

3) Sync the changes with AWS

NB: you can use the ```--dryrun``` command line option to see what will happen without actually executing anything.

Test server:
```bash
aws s3 sync /Volumes/websites/iiesidev/ s3://test.iiesi.org --exclude ".git/*" --exclude "*.DS_Store" --delete
```

Prod server:
```bash
aws s3 sync /Volumes/websites/iiesidev/ s3://iiesi.org --exclude ".git/*" --exclude "*.DS_Store" --delete
```


If you're using the s3cmd command set:

Test server:
```
s3cmd sync /Volumes/websites/iiesidev/ s3://test.iiesi.org --acl-public --exclude ".git/*" --delete-removed --verbose
```

Prod server:
```
s3cmd sync /Volumes/websites/iiesidev/ s3://iiesi.org --acl-public --exclude ".git/*" --delete-removed --verbose
```
