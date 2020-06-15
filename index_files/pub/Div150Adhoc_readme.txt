-----------------------
Div150Adhoc - Dataset readme
-----------------------

----------
**Authors: 
Bogdan Ionescu, LAPI, University Politehnica of Bucharest, Romania (bogdanLAPI@gmail.com);
Alexandru Lucian Gînsca, CEA LIST, France (alexandru.ginsca@cea.fr); 
Maia Zaharieva, University of Vienna & Vienna University of Technology, Austria (maia.zaharieva@univie.ac.at);
Bogdan Boteanu, LAPI, University Politehnica of Bucharest, Romania (bboteanu@alpha.imag.pub.ro);
Mihai Lupu, Vienna University of Technology, Austria (lupu@ifs.tuwien.ac.at); 
Henning Müller, University of Applied Sciences Western Switzerland (HES-SO) in Sierre, Switzerland (henning.mueller@hevs.ch).

This dataset was partially supported by the Vienna Science and Technology Fund (WWTF) through project ICT12-010.

Many thanks to Gabi Constantin, Lukas Diem, Ivan Eggel, Laura Flueratoru, Ciprian Iona?cu, Corina Macovei, Catalin Mitrea, Irina Emilia Nicolae, Mihai Gabriel Petrescu, Andrei Purica for their help.


----------
**Citation:
B. Ionescu, A.L. Gînsca, M. Zaharieva, B. Boteanu, M. Lupu, H. Müller, "Retrieving Diverse Social Images at MediaEval 2016: Challenge, Dataset and Evaluation", MediaEval Benchmarking Initiative for Multimedia Evaluation, vol. 1739, CEUR-WS.org, ISSN: 1613-0073, Hilversum, Netherlands, October 20-21, 2016.


----------
**Description:
The dataset consists of 70 multi-concept queries and 20,757 images for development (devset; 35 location-related multi-concept queries from the 2015 testset and 35 general-purpose multi-concept queries) and 65 general-purpose multi-concept queries and 19,017 images for testing (testset).

For each query in devset and testset, the following information is provided:
- query text formulation: is the actual query formulation used on Flickr to retrieve all the data;
- query title: is the unique query text identifier - this is basically the query text formulation from which spaces and special characters have been removed (please note that all the query related resources are indexed using this text identifier);
- query id: each query has an unique query id code to be used for preparing the official runs (i.e., numbers from 1 to 135 - the total number of queries; numbers from 1 to 70 are belonging to the devset queries and the rest to the testset queries);
- a set of photos retrieved from Flickr in jpeg format (up to 300 photos per query - each photo is named according to its unique id from Flickr). Photos are stored in individual folders named after the query title;
- an xml file containing metadata from Flickr for all the retrieved photos;
- visual, text and credibility descriptors;
- ground truth for both relevance and diversity.

---Important--: please note that all the photos provided are under Creative Commons licenses that allow redistribution. Each Flickr photo is provided with the license type and the owner’s name.


----------
**XML metadata
Each query in devset and testset is accompanied by an xml file (UTF-8 encoded) that contains all the retrieved metadata for all the photos. Each file is named after the query title, e.g., “acropolis_athens.xml” for query "Acropolis Athens". The information is structured as follows:

<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<photos topic="acropolis athens">
<photo date_taken="2013-06-04 02:45:20" description="View of Athens from the entrance of Acropolis" id="9067739127" latitude="37.970805" license="2" longitude="23.721167" rank="1" tags="athens greece" title="Acropolis - Athens" url_b="http://farm8.static.flickr.com/7362/9067739127_edda2711ca_b.jpg" username="pfischermx" userid="56505984@N06" views="70"/>
...
</photos>

The topic value is the query text formulation used to retrieve data from Flickr. Each of the photos is described by a <photo> element. Among the photo information fields, please note in particular:
- description contains a detailed textual description of the photo as provided by the author;
- id is the unique identifier of each photo from Flickr and corresponds to the name of the jpeg file associated to this photo (e.g., 9067739127 corresponds to file 9067739127.jpg); 
- license is the Creative Common license of this picture; 
- rank is the position ranking of the photo in the list retrieved from Flickr (a generated number from 1 to the number of photos);
- tags are the tag keywords (space-separated) used for indexing purpose;
- title is a short textual description of the photo provided by the author;
- url_b is the url link of the photo location from Flickr (please note that by the time you use the dataset some of the photos may not be available anymore at the same location);
- username represent the photo owner’s name;
- userid is the unique user id from Flickr;
- views is the number of times the photo has been viewed on Flickr.



----------
**CNN-based descriptors
For each query and photo we provide also some convolutional neural network based descriptors, namely:
- CNN generic (code cnn_gen - 4,096 values): descriptor based on the reference convolutional (CNN) neural network model provided along with the Caffe framework. This model is learned with the 1,000 ImageNet classes used during the ImageNet challenge. The descriptors are extracted from the last fully connected layer of the network (named fc7);
- CNN adapted (code cnn_ad - 4,096 values): descriptor based on a CNN model obtained with an identical architecture to that of the Caffe reference model. This model is learned with 1,000 tourist points of interest classes whose images were automatically collected from the Web. Similar to CNN generic, the descriptors are extracted from the last fully connected layer of the network (named fc7). For more details see [v7]. Please note that adaptation is done only for the 2015 location based multi-topic queries (35 queries from devset). For the other queries, the descriptor is computed as the generic one, because queries are diverse enough and do not require any adaptation. 

File format. Descriptors are provided on a per query basis. We provide individual csv (comma-separated values) files for each type of visual descriptor and for each query. The naming convention is the following: query title followed by the descriptor code, e.g., “acropolis_athens cnn_ad.csv” refers to the CNN adapted descriptor for the query acropolis_athens. Each file contains the descriptors for each of the photos of the query on one line. The first value of each line is the unique photo id followed by the descriptor values separated by commas. Lines are separated by an end-of-line character (carriage return). An example is presented below:

3338743092,0.51934475780470812,0.40031641870181739,...
3338745530,0.20630411506897756,0.26843536114050304,...
3661394189,0.47248077522064869,0.17833862284689939,...
...


----------
**Textual descriptors
Text descriptors are provided on per dataset basis. For each set (i.e., devset, testset), the text descriptors are computed on: per image basis (file [dataset]_textTermsPerImage.txt), per query basis (file [dataset]_textTermsPerTopic.txt) and per user basis, respectively (file [dataset]_textTermsPerUser.txt).

File format. In each file, each line represents an entity with its associated terms and their weights. For instance, in the devset per image basis descriptor file (devset_textTermsPerImage.txt) a line will look like:

9067739127 "acropoli" 2 299 0.006688963210702341 "athen" 3 304 0.009868421052631578 "entrance" 1 130 0.007692307692307693 "greece" 1 257 0.0038910505836575876 "view" 1 458 0.002183406113537118
...

The first token is the id of the entity, in this case the unique Flickr id of the image. Following that is a list of 4-tuples ("term" TF DF TF-IDF), where "term" is a term which appeared anywhere in the description, tags or title of the image from the metadata, TF is the term frequency (the number of occurrences of the term in the entity's text fields), the DF is the document frequency (the number of entities which have this term in their text fields) and finally the TF-IDF is simply TF/DF [t1]. The information from the query-based text descriptors is the same as in the image-based case except for the fact that the entity here is the query. Its textual description is taken to be the set of all texts of all of its images. The information from the user-based text descriptors is also similar except for the fact that the entity here is the photo user id from Flickr. Its textual description is taken to be the set of all texts of all of her images, regardless of the query. These query-based and user-based text descriptors are important because they tell us what terms are commonly used to refer to a query or are common across all queries, and what terms are generally used by a user and which ones by all users. 

SOLR Indexes
The term lists provided and described above were generated using Solr 6.0.0. To make it easier for all the participants to get a baseline system for text retrieval, we also provide all the details to get your own Solr server running, containing all the data necessary for retrieving images, out of the box. First download Solr from http://lucene.apache.org/. We have used version 6.0.0 in generating the files here. Assuming you have decompressed the archive solrCores.zip in /my/path/solrCores start Solr by running the command:

bash#> /path/to/solr/bin/solr -s /my/path/solrCores

You should now be able to access it at localhost:8983.

Additionally, we provide participants with a data folder which has all the data provided, but in a format ingestible by Solr and which can be used with the post2solr.sh script to generate new indexes, with different pre-processing steps or similarity functions. We also provide the scripts that were used to generate the text feature files from the solr indexes (makeTermList.sh). All scripts are Bash scripts, so they should run in most *ix systems, but not under Windows. The contents of this folder is:
- scripts to generate the term lists out of the Solr indexes (makeTermList.sh and makeTermLists.sh);
- scripts to populate the solr indexes with data (post2solr.sh, post2solr1file.sh, and post2solrs.sh);
- archive with solr cores (solrCore.zip);
- folder with data in a format used by post2solr scripts above (solrIngestableData);
- the text feature files, generated by the makeTermLists.sh above (textFeatureFiles).


----------
**Wikiset Data

In addition to the text models provided with the data, we also provide semantic vectors for general English terms, computed using Word2Vec on top of the English Wikipedia which could help the participants in developing advanced text models. In processing the Wikipedia text, no stemming has been applied. We provide both normalized and non-normalized vectors for dimensionalities 50, 100, 200, 300, and 400. Each file is simply a set of rows, each row consisting of the term followed by a set of 50, 100, 200, 300, and 400 floating point values. In absence of any additional consideration, we recommend using the 200 or 300 dimensionality vectors. Generally one uses the cosine similarity between vectors to estimate the conceptual similarity, but for these vectors this is more a result of unchallenged common practice than a scientifically grounded method. Here is an example of one file:

no 0.007619 -0.493089 0.264928 …
season 0.512420 0.079815 0.264437 …
became 0.178607 -0.364249 0.319318 …
south 0.078578 -0.209191 0.492709 …
...

Filenames with "norm" have normalized these values (the sum of the elements on each row is 1).

Wikiset files. The following files are provided in the wikiset folder:
- vectorXX-1.txt.norm.zip - containing the normalized data; 
- vectorXX-1.txt.zip - containing the non-normalized data.
*XX is 50, 100, 200, 300, or 400 (the dimensionality of the vectors).


----------
**User annotation credibility descriptors
We provide user tagging credibility descriptors that give an automatic estimation of the quality of tag-image content relationships. The aim of credibility descriptors is to give participants an indication about which users are most likely to share relevant images in Flickr (according to the underlying task scenario). These descriptors are extracted by visual or textual content mining:
- visualScore: descriptor obtained through visual mining using over 17,000 of ImageNet visual models obtained by learning a binary SVM per ImageNet concept. Visual models are built on top of overfeat, a powerful convolutional Neural Network feature [c1]. At most 1,000 images are downloaded for each user in order to compute visualScores. For each Flickr tag which is identical to an ImageNet concept, a classification score is predicted and the visualScore of a user is obtained by averaging individual tag scores. The intuition here is that the better the predictions given by the classifiers are, the more relevant a user’s images should be. Scores are normalized between 0 and 1, with higher scores corresponding to more credible users;
- faceProportion: descriptor obtained using the same set of images as for visualScore. The default face detector from OpenCV [c2] is used here to detect faces. faceProportion, the percentage of images with faces out of the total of images tested for each user is computed. The intuition here is that the lower faceProportion is, the better the average relevance of a user’s photos is. faceProportion is normalized between 0 and 1, with 0 standing for no face images;
- tagSpecificity: descriptor obtained by computing the average specificity of a user’s tags. Tag specificity is calculated as the percentage of users having annotated with that tag in a large Flickr corpus (~100 million image metadata from 120,000 users);
- locationSimilarity: descriptor obtained by computing the average similarity between a user's geotagged photos and a probabilistic model of a surrounding cell of approximately 1 km2 geotagged images. These models were created for MediaEval 2013 Placing Task [c3] and reused as such here. The intuition here is that the higher the coherence between a user’s tags and those provided by the community is, the more relevant her images are likely to be. locationSimilarity is not normalized and small values stand for the lowest similarity;
- photoCount: descriptor which accounts for the total number of images a user shared on Flickr. This descriptor has a maximum value of 10,000;
- uniqueTags: proportion of unique tags present in a user's vocabulary divided by the total number of tags of the user. uniqueTags ranges between 0 and 1;
- uploadFrequency: average time between two consecutive uploads in Flickr. This descriptor is not normalized;
- bulkProportion: the proportion of bulk taggings in a user’s stream (i.e., of tag sets which appear identical for at least two distinct photos). The descriptor is normalized between 0 and 1;
- meanPhotoViews: the mean value of the number of times a user's image has been seen by other members of the community. This descriptor is not normalized;
- meanTitleWordCounts: the mean value of the number of words found in the titles associated with users' photos. This descriptor is not normalized;
- meanTagsPerPhoto: the mean value of the number of tags users put for their images. This descriptor is not normalized;
- meanTagRank: the mean rank of a user's tags in a list in which the tags are sorted in descending order according the the number of appearances in a large subsample of Flickr images. We eliminate bulk tagging and obtain a set of 20,737,794 unique tag lists out of which we extract the tag frequency statistics. To extract this descriptor we take into consideration only the tags that appear in the top 100,000 most frequent tags. This descriptor is not normalized;
- meanImageTagClarity: this descriptor is based on an adaptation of the Image Tag Clarity score described in [c4]. The clarity score for a tag is the KL-divergence between the tag language model and the collection language model. We use the same collection of 20,737,794 unique tag lists to extract the language models. The collection language model is estimated by the relative tag frequency in the entire collection. Unlike [c4], for the individual tag language model, we use a tf/idf language model, more in the lines of a classical language models. For a target tag, we consider a "document" the subset of tag lists that contain the target tag. For a tag, its clarity score is an indicator on the diversity of contexts the tag is used. A low clarity score suggest a tag is generally used together with the same tags. meanImageTagClarity is the mean value of the clarity score of a user's tags.  To extract this descriptor, we take into consideration only the tags that appear in the top 100,000 most frequent tags. This descriptor is not normalized.

File format. Descriptors are provided on a per user basis. We provide separate XML files for each user and in each file we include separate fields for the credibility descriptors enumerated above. XML files have the following format:

<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<metadata user="21953562@N07">
<credibilityDescriptors>
<visualScore>0.791442635512724</visualScore>
<faceProportion>0.013</faceProportion>
<tagSpecificity>0.624967978500227</tagSpecificity>
<locationSimilarity>1.52020128875995</locationSimilarity>
<photoCount>6710</photoCount>
<uniqueTags>0.05555555555555555</uniqueTags>
<uploadFrequency>395.91869026284303</uploadFrequency>
<bulkProportion>0.8785394932935916</bulkProportion>
...
</credibilityDescriptors>
</metadata>

User annotation credibility descriptors are separated by <credibilityDescriptors> </credibilityDescriptors> statements. 


----------
**Topic files
For each dataset we provide a topic file that contains the list of the queries in the current dataset. Each query is delimited by a <topic> </topic> statement and includes the query id code (delimited by a <number> </number> statement), and the query title (delimited by a <title> </title> statement). An example is presented below:

<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<topics>
<topic>
    <number>26</number>
    <title>Abbey of Saint Gall</title>
    <latitude></latitude>
    <longitude></longitude>
    <wiki></wiki>
</topic>
...
</topics>


----------
**Ground truth
The ground truth data consists on relevance ground truth (code rGT) and diversity ground truth (code dGT and dclusterGT). Ground truth was generated by a small group of expert annotators with advanced knowledge of the query characteristics (mainly learned from Internet sources). Each type of ground truth consisted on a different protocol and followed the exact definitions adopted for this scenario:
- Relevance: a photo is considered to be relevant for the query if it is a common photo representation of the query topics (all at once). Bad quality photos (e.g., severely blurred, out of focus, etc.) are not considered relevant in this scenario;
- Diversity: a set of photos is considered to be diverse if it depicts different visual characteristics of the query topics and subtopics with a certain degree of complementarity, i.e., most of the perceived visual information is different from one photo to another.

Relevance ground truth was annotated using a dedicated tool that provided the annotators with one photo at a time. A reference photo of the location could be also displayed during the process. Annotators were asked to classify the photos as being relevant (score 1), non-relevant (score 0) or with “don’t know” answer (score -1). The definition of relevance was available to the annotators in the interface during the entire process. The annotation process was not time restricted. Annotators were recommended to consult any additional information source about the characteristics of the location (e.g., from Internet) in case they were unsure about the annotation. Ground truth was collected from several annotators and final ground truth was determined after a lenient majority voting scheme.

File format. Ground truth is provided to participants on a per query basis. We provide individual txt files for each query. Files are named according to the query title followed by the ground truth code, e.g., “abbey_of_saint_gall rGT.txt” refers to the relevance ground truth (rGT) for the query abbey_of_saint_gall. Each file contains photo ground truth on individual lines. The first value of each line is the unique photo id followed by the ground truth value separated by comma. Lines are separated by an end-of-line character (carriage return). An example is presented below:

3338743092,1
3338745530,0
3661394189,1
...

Diversity ground truth was also annotated with a dedicated tool. The diversity is annotated only for the photos that were judged as relevant in the previous step. For each query, annotators were provided with a thumbnail list of all the relevant photos. The first step required annotators to get familiar with the photos by analyzing them for about 5 minutes. Next, annotators were required to re-group the photos into similar visual appearance clusters. Full size versions of the photos were available by clicking on the photos. The definition of diversity was available to the annotators in the interface during the entire process. For each of the clusters, annotators provided some keyword tags reflecting their judgments in choosing these particular clusters. Similar to the relevance annotation, the diversity annotation process was not time restricted. In this particular case, ground truth was collected from several annotators that annotated distinct parts of the data set.

File format. Ground truth is provided to participants on a per query basis. We provide two individual txt files for each query: one file for the cluster ground truth and one file for the photo diversity ground truth. Files are named according to the query title followed by the ground truth code, e.g., “abbey_of_saint_gall dclusterGT.txt” and “abbey_of_saint_gall dGT.txt” refer to the cluster ground truth (dclusterGT) and photo diversity ground truth (dGT) for the query abbey_of_saint_gall.

In the dclusterGT file each line corresponds to a cluster where the first value is the cluster id number followed by the cluster user tag separated by comma. Lines are separated by an end-of-line character (carriage return). An example is presented below:

1,outside statue
2,inside views
3,partial frontal view
4,archway
...

In the dGT file the first value on each line is the unique photo id followed by the cluster id number (that corresponds to the values in the dclusterGT file) separated by comma. Each line corresponds to the ground truth of one image and lines are separated by an end-of-line character (carriage return). An example is presented below:

3664415421,1
3665220244,1
...
3338745530,2
3661396665,2
...
3662193652,3
3338743092,3
3665213158,3
...


----------
**MediaEval submission format

The following information will help reproducing the exact evaluation conditions of the MediaEval task. At MediaEval runs were provided in the form of a trec topic file. This file is compatible with the trec_eval evaluation software (for more information please follow the link http://trec.nist.gov/trec_eval/index.html – you will find two archives trec_eval.8.1.tar.gz and trec_eval_latest.tar.gz - see the README file inside). The trec topic file has the structure illustrated by the following example of a file line (please note that values are separated by whitespaces):

030 Q0 ZF08 0 4238 prise1
qid iter docno rank sim run_id

where:
- qid is the unique query id (please note that each query has a certain query id code that is provided with the data set in the topic xml files – see Data section); 
- iter – is ignored; 
- docno – is the unique photo id (as provided with the data set); 
- rank – is the photo rank in the refined list provided by your method. Rank is expected to be an integer value ranging from 0 (the highest rank) up to 49 (see the Goal of task section); 
- sim – is the similarity score of your photo to the query and is mandatory for the submission. The similarity values need to be higher for the photos to be ranked first and should correspond to your refined ranking (e.g., the photo with rank 0 should have the highest sim value, followed by photo with rank 1 with the second highest sim value and so on). In case your approach do not provide explicitly similarity scores (e.g., crowd-sourcing) you are required to create dummy similarity scores that decrease when the rank increases (e.g., in this case, you may use the inverse ranking values); 
- run_id - is the name of your run (which you can choose, but should be as informative as possible without being too long – please note that no whitespaces or other special characters are allowed).

Please note that each run needs to contain at least one result for each location. An example of results file should look like this:

1 0 3338743092 0 0.94 run1_audiovisualRF
1 0 3661411441 1 0.9 run1_audiovisualRF
...
1 0 7112511985 48 0.2 run1_audiovisualRF
1 0 711353192 49 0.12 run1_audiovisualRF
2 0 233474104 0 0.84 run1_audiovisualRF
2 0 3621431440 1 0.7 run1_audiovisualRF
...

  
----------
**Scoring tool 
The official MediaEval scoring tool is div_eval.jar. It computes cluster recall at X (CR@X --- a measure that assesses how many different clusters from the ground truth are represented among the top X results), precision at X (P@X --- measures the number of relevant photos among the top X results) and their harmonic mean, i.e., F1-measure@X (X in {5,10,20,30,40,50}).

The software tool was developed under Java and to run it you need to have Java installed on your machine. To check, you may run the following line in a command window: "java -version". In case you don't have Java installed, please visit this link, download the Java package for your environment and install it.

To run the script, use the following syntax (make sure you have the div_eval.jar file in your current folder):

java -jar div_eval.jar -r <runfilepath> -rgt <rGT directory path> -dgt <dGT directory path> -t <topic file path> -o <output file directory> [optional: -f <output file name>]

where:
-r <runfilepath> - specifies the file path to the current run file for which you want to compute the evaluation metrics;
-rgt <rGT directory path> - specifies the path to the relevance ground truth (denoted by rGT) for the current data set;
-dgt <dGT directory path> - specifies the path to the diversity ground truth (denoted by dGT) for the current data set;
-t <topic file path> - specifies the file path to the topic xml file for the current data set;
-o <output file directory> - specifies the path for storing the evaluation results. Evaluation results are saved as .csv files (comma separated values);
-f <output file name> - is optional and specifies the output file name. By default, the output file will be named according to the run file name + "_metrics.csv".

Run example:

java -jar div_eval.jar -r c:\divtask\RUNd2.txt -rgt c:\divtask\rGT -dgt c:\divtask\dGT -t c:\divtask\devset_topics.xml -o c:\divtask\results –f my_first_results

Output file example:

--------------------
"Run name","RUNd2.txt"
--------------------
"Average P@20 = ",.784
"Average CR@20 = ",.4278
"Average F1@20 = ",.5432
--------------------
"Query Id ","Location name",P@5,P@10,P@20,P@30,P@40,P@50,CR@5,CR@10,CR@20,CR@30,CR@40,CR@50,F1@5,F1@10,F1@20,F1@30,F1@40,F1@50
1,"Aachen Cathedral",.8,.9,.95,.9667,.95,.94,.1333,.4,.5333,.7333,.8667,.9333,.2286,.5538,.6831,.834,.9064,.9367
2,"Angel of the North",1.0,.9,.95,.9333,.925,.94,.2667,.5333,.8,.8667,.8667,.9333,.4211,.6698,.8686,.8988,.8949,.9367
...
24,"Acropolis of Athens",.6,.8,.85,.8667,.875,.88,.25,.5,.6667,.6667,.8333,.8333,.3529,.6154,.7473,.7536,.8537,.856
25,"Ernest Hemingway House",.8,.7,.5,.5667,.55,.6,.2353,.4118,.5294,.6471,.7647,.8824,.3636,.5185,.5143,.6042,.6398,.7143
--------------------
"--","Avg.",P@5,P@10,P@20,P@30,P@40,P@50,CR@5,CR@10,CR@20,CR@30,CR@40,CR@50,F1@5,F1@10,F1@20,F1@30,F1@40,F1@50
,,.76,.784,.792,.784,.789,.7944,.2577,.4278,.6343,.7443,.8504,.8919,.376,.5432,.696,.757,.813,.834


----------
**References:
[v7] Spyromitros-Xioufis, E., Papadopoulos, S., Ginsca, A., Popescu, A., Kompatsiaris, I., Vlahavas, I. Improving Diversity in Image Search via Supervised Relevance Scoring. ACM International Conference on Multimedia Retrieval, ACM, Shanghai, China, 2015.
[t1] Wu, H.C., Luk, R.W.P., Wong, K.F., Kwok, K.L. Interpreting TF–IDF Term Weights As Making Relevance Decisions. ACM Transactions on Information Systems, Vol 26 (3), 2008, 1 - 37.
[c1] Overfeat home page: http://cilvr.nyu.edu/doku.php?id=code:start.
[c2] OpenCV face detector: http://docs.opencv.org/trunk/doc/py_tutorials/py_objdetect/py_face_detection/py_face_detection.html.
[c3] Popescu, A. CEA LIST’s Participation at MediaEval 2013 Placing Task, Working Notes of MediaEval 2013, CEUR-WS, Vol. 1043, ISSN 1613-0073, Barcelona, Spain.
[c4] Sun, A., Bhowmick, S.S. Image tag clarity: in search of visual-representative tags for social images. SIGMM workshop on Social media, ACM, 2009.



