# PySpark-on-GoogleColab
A Beginner’s Hands-on Guide to PySpark with Google Colab-Tutorial Notebook From Scratch

1- Use !wget to download the dataset to the server
Colab is actually a Centos virtual machine with GPU. You can directly use the linux wget command to download the dataset to the server. The default is to download to the /content path

Download and unzip the dataset command:

[ ]
#!wget https://download.pytorch.org/tutorial/hymenoptera_data.zip
#!unzip hymenoptera_data.zip -d ./
Load dataset command:

[ ]
# Define the dataset using ImageFolder
# define data preprocessing
#train_tf = tfs.Compose([
 #  tfs.RandomResizedCrop(224),
 #  tfs.RandomHorizontalFlip(),
 #  tfs.ToTensor(),
 #  tfs.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225]) # Use ImageNet mean and variance
#])
#train_set = ImageFolder('./hymenoptera_data/train/', train_tf)
2- Loading data into PySpark from github
Spark has a variety of modules to read data of different formats. It also automatically determines the data type for each column, but it has to go over it once.

For this article, I have created a sample JSON dataset in Github. You can download the file directly into Colab using the ‘wget’ command like this:


#!wget --continue https://raw.githubusercontent.com/GarvitArya/pyspark-
#demo/main/sample_books.json -O /tmp/sample_books.json
Now read this file into a Spark dataframe using the read module.


#df = spark.read.json("/tmp/sample_books.json")

3- Use Google Cloud Disk to load datasets
First, the command to mount Google Cloud Disk in Colab is as follows. After execution, you will be asked to enter the key of your Google account to mount


#from google.colab import drive
#drive.mount('/content/drive/')
Upload the file to Google Drive, such as data/data.csv. One way to upload is to upload manually, the other is to download to Google Cloud Disk through the wget command, and then load it for use

The advantage of storing in Google Cloud Disk is that the data will not be lost the next time you connect like the first method. The disadvantage is that The Google cloud disk is only 15g, which is not suitable for large data sets. The command to download the data set to the Google cloud disk is as follows:


#import os
#Change the current working directory to the path of Google Cloud Drive
#path="/content/drive/My Drive/Colab Notebooks/"
#os.chdir(path)
#os.listdir(path)
#Use the wget command to download the dataset to this path
#!wget https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/data.csv
Load dataset


#train = pd.read_csv('/content/drive/My Drive/Colab Notebooks/data/data.csv')

4. Load dataset from kaggle
If you are playing a game on kaggle, the data set you need is prepared on it, and you can download it directly using the kaggle command. You need to choose to create an api token in the my profile of kaggle, and then generate the username and key locally


#{"username":"gongenbo","key":"f26dfa65d06321a37f6b8502cd6b8XXX"}

Command to download data via kaggle


#!pip install -U -q kaggle
#!mkdir -p ~/.kaggle
#!echo '{"username":"gongenbo","key":"f26dfa65d06321a37f6b8502cd6b8XXX"}' > ~/.kaggle/kaggle.json
#!chmod 600 ~/.kaggle/kaggle.json
#!kaggle competitions download -c state-farm-distracted-driver-detection
Command to submit scores to kaggle after training


#!kaggle competitions submit -c state-farm-distracted-driver-detection -f submission.csv -m "Message"

5. Upload to disk using the upload button
Google provides 67G of disk space. Use the upload button to upload the image below. This method is suitable for small datasets or own datasets:

1111.png

6-There is a library in jovian called open datasets.
First, install it into colab using- The URL can be any link be it google or kaggle links.


#!pip install opendatasets --upgrade
#import opendatasets as od
#dataset_url = 'https://www.kaggle.com/tunguz/us-elections-dataset'
#od.download(dataset_url)
Reference:

https://stackoverflow.com/questions/71619540/how-to-upload-a-62-gb-datasets-to-google-colab https://blog.devgenius.io/get-started-with-pyspark-and-google-colab-notebook-in-4-minutes-94b4e2cecad7
