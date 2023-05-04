Download Link: https://assignmentchef.com/product/solved-csci572-homework3-inverted-index-objectives
<br>
<strong>Hadoop Exercise to Create an Inverted Index Objectives: </strong>

<ul>

 <li><strong>Creating an Inverted Index of words occurring in a set of web pages</strong></li>

 <li><strong>Get hands-on experience in GCP App Engine</strong></li>

</ul>

We’ll be using a subset of 74 files from a total of 408 files (text extracted from HTML tags) derived from the Stanford WebBase project that is available <a href="https://ebiquity.umbc.edu/resource/html/id/351">here.</a> It was obtained from a web crawl done in February 2007. It is one of the largest collections totaling more than 100 million web pages from more than 50,000 websites. This version has been cleaned for the purpose of this assignment.

These files will be placed in a bucket on your Google cloud storage and the Hadoop job will be instructed to read the input from this bucket.

<ol>

 <li>Uploading the input data into the bucket</li>

 <li>Get the data files from either of the links below http://www-scf.usc.edu/~csci572/2020Spring/hw3/DATA.zip</li>

</ol>

<a href="https://drive.google.com/drive/u/1/folders/1Z4KyalIuddPGVkIm6dUjkpD_FiXyNIcq">https://drive.google.com/drive/u/1/folders/1Z4KyalIuddPGVkIm6dUjkpD_FiXyNIcq</a>

You may use your USC account to get access to the data from the Google Drive link. Compressed full data is around 1.1GB. Uncompressed, it is 3.12 GB of data for the files for this project. So on balance you should download the zipped file, not the folder.

<ol>

 <li>Unzip the contents. You will find two folders inside named <strong>‘development’</strong> and ‘<strong>full data</strong>’. Each of the folders contains the actual data (txt files). We suggest you use the development data initially while you are testing your code. Using the full data will take up to few minutes for each run of the Map-Reduce job and you may risk spending all your cloud credits while testing the code.</li>

 <li>Click on ‘Dataproc’ in the left navigation menu under . Next, locate the address of the default<strong> Google cloud storage staging</strong> bucket for your cluster in the Figure 1 below. If you’ve previously disabled billing, you need to re-enable it before you can upload the data. Refer to the <strong>“Enable and Disable Billing account”</strong> section to see how to do this. d.</li>

</ol>

<strong>                                                Figure 1:</strong> The default Cloud Storage bucket.

<ol>

 <li>Go to the storage section in the left navigation bar and select your cluster’s default bucket from the list of buckets. At the top you should see menu items UPLOAD FILES, UPLOAD FOLDER, CREATE FOLDER, etc (Figure 2). Click on the UPLOAD FOLDER button and upload the dev_data folder and full_data folder individually. This will take a while, but there will be a progress bar (Figure 3). You may not see this progress bar as soon as you start the upload but, it will show up eventually.</li>

</ol>

<strong>Figure 2: </strong>Cloud Storage Bucket.

<strong>Figure 3</strong>: Progress of uploading

<h1>Inverted Index Implementation using Map-Reduce</h1>

Now that you have the cluster and the files in place, you need to write the actual code for the job. As of now, Google Cloud allows us to submit jobs via the UI, only if they are packaged as a jar file. The following steps are focused on submitting a job written in Java via the Cloud console UI.

Refer to the examples below and write a Map-Reduce job in java that creates an Inverted Index given a collection of text files. You can very easily tweak a <strong>word-count example</strong> to create an inverted index instead

(<strong>Hint</strong>: Change the mapper to output word <strong>docID</strong> instead of word count and in the reducer use a <strong>HashMap</strong>).

Here are some helpful examples of Map-Reduce Jobs

<ol>

 <li><a href="https://developer.yahoo.com/hadoop/tutorial/module4.html#wordcount">https://developer.yahoo.com/hadoop/tutorial/module4.html#wordcount</a></li>

 <li><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">https://hadoop.apache.org/docs/stable/hadoop</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">–</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">mapreduce</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">–</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">client/hadoop</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">–</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">mapreduce</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">–</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">client</a><a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html">core/MapReduceTutorial.html</a></li>

</ol>

The example in the following pages explains a Hadoop word count implementation in detail. It takes one text file as input and returns the word count for every word in the file. Refer to the comments in the code for explanation.

<strong>The Mapper Class:</strong>

<strong>The Reducer Class:</strong>

<strong>Main Class </strong>

The input data is cleaned, that is all the 
r s is removed but one or more t might still be present (which needs to be handled). There will be punctuation and you are required to handle this in your code. Replace all the occurrences of special characters and numerals by space character, convert all the words to the lowercase.  The ‘t’ separates the key(Document ID) from the value(Document). The input files are in a key value format as below:




<table width="281">

 <tbody>

  <tr>

   <td width="151">DocumentID</td>

   <td width="130">document</td>

  </tr>

 </tbody>

</table>




Sample document:

The mapper’s output is expected to be as follows:

The above example indicates that the word aspect occurred 1 time in the document with docID 5722018411 and economics 2 times.

The reducer takes this as input, aggregates the word counts using a Hashmap and creates the Inverted index. The format of the index is as follows.

<table width="489">

 <tbody>

  <tr>

   <td width="199">word docID:count</td>

   <td width="144">docID:count</td>

   <td width="146">docID:count…</td>

  </tr>

 </tbody>

</table>




The above sample shows a portion of the inverted index created by the reducer.

To write the Hadoop java code you can use the <strong>VI</strong> or <strong>nano</strong> editors that come pre-installed on the master node. You can test your code on the cluster itself. Be sure to use the development data while testing the code. You are expected to write a simple Hadoop job. You can just tweak <a href="https://hadoop.apache.org/docs/stable/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html#Example:_WordCount_v1.0">this</a> example if you’d like, but make sure you understand it first.

<h1>Creating a jar for your code</h1>

Now that your code for the job is ready we’ll need to run it. The Google Cloud console requires us to upload a Map-Reduce job as a jar file. In the following example the Mapper and Reducer are in the same file called InvertedIndexJob.java.To create a jar for the Java class implemented please follow the instructions below. The following instructions were executed on the cluster’s master node on the Google Cloud.

<ol>

 <li>Say your Java Job file is called InvertedIndex.java. Create a JAR as follows:</li>

</ol>

○ hadoop com.sun.tools.javac.Main InvertedIndexJob.java

If you get the following Notes you can ignore them

Note: InvertedIndexJob.java uses or overrides a deprecated API.

Note: Recompile with -Xlint:deprecation for details.

○ jar cf invertedindex.jar InvertedIndex*.class

Now you have a jar file for your job. You need to place this jar file in the default cloud bucket of your cluster. Just create a folder called JAR on your bucket and upload it to that folder. If you created your jar file on the cluster’s master node itself use the following commands to copy it to the JAR folder.

○ hadoop fs -copyFromLocal ./invertedindex.jar

○ hadoop fs -cp ./invertedindex.jar gs://dataproc-69070…/JAR




The highlighted part is the default bucket of your cluster. It needs to be prepended by the gs:// to tell the Hadoop environment that it is a bucket and not a regular location on the filesystem.

<strong><u>Note</u></strong>: This is not the only way to package your code into a jar file. You can follow any method that will create a single jar file that can be uploaded to the Google cloud.