
# LAB- Console and Cloud Shell
## Objectives
In this lab, you learn how to perform the following tasks:
- Create a Cloud Storage bucket using the Cloud Console.
- Create a Cloud Storage bucket using Cloud Shell.
- Become familiar with Cloud Shell features.

### Task 1 

Create a Cloud Storage bucket using the Cloud Console.
```
$ gsutil mb gs://mathapelo
```
### Task 2

Create a Cloud Storage bucket using Cloud Shell.
```
 $ gsutil mb gs://mathapelo-2
```

### Task 3
Explore more Cloudshell features:
1. Move a document between pc and gcloud.
```
$ gcloud alpha cloud-shell scp localhost:~/translate.md cloudshell:~translate.md
```
2. Check if the document has been transterred to cloud.
```
$ls
```
3. Copy document to one of the created buckets
```
$ gsutil cp translate.md  gs://mathapelo-2
```

### Task 4

Create a persistent state in Cloud Shell


1. List available regions
```
gcloud compute regions list
```
Select a region from the list and note the value in any text editor. This region will now be referred to as [YOUR_REGION] in the remainder of the lab.


2. Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:
```
INFRACLASS_REGION=us-central1
```
3. Verify it with echo:
```
echo $INFRACLASS_REGION
```
4. Create a subdirectory for materials used in this class:
```
mkdir infraclass
```
5. Create a file called config in the infraclass directory:
```
touch infraclass/config
```

6. Append the value of your Region environment variable to the config file:
```
echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config
```
7. Create a second environment variable for your Project ID, replacing [YOUR_PROJECT_ID] with your Project ID. You can find the project ID on the Cloud Console Home page.
```
INFRACLASS_PROJECT_ID=qwiklabs-gcp-00-98fab5e497f3
```
8. Append the value of your Project ID environment variable to the config file:
```
echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config
```
9. Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:
```
$ source infraclass/config
$ echo $INFRACLASS_PROJECT_ID
```
This gives you a method to create environment variables and to easily recreate them if the Cloud Shell is cycled. However, you will still need to remember to issue the source command each time Cloud Shell is opened.

In the next step you will modify the .profile file so that the source command is issued automatically any time a terminal to Cloud Shell is opened.

Close and re-open Cloud Shell. Then issue the echo command again:
```
$ echo $INFRACLASS_PROJECT_ID
```
There will be no output because the environment variable no longer exists.

Modify the bash profile and create persistence
Edit the shell profile with the following command:
```
$ nano .profile
```
Add the following line to the end of the file:
```
source infraclass/config
```
Press Ctrl+O, ENTER to save the file, and then press Ctrl+X to exit nano.

Close and then re-open Cloud Shell to cycle the VM.

Use the echo command to verify that the variable is still set:
```
echo $INFRACLASS_PROJECT_ID
```
You should now see the expected value that you set in the config file.



