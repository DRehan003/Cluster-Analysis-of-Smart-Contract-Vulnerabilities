<h1> Cluster Analysis of Smart Contract Vulnerabilities </h1>

Objective: Perform cluster analysis on a dataset of smart contracts in Python to identify similar risk profiles through the use of the pandas, numpy, matplotlib, seaborn, and scipy libraries. <br>
<br>
Essential Terminology:
- __Smart Contract__: A self-executing program  stored on blockchain that automatically carries out an agreement when certain conditions are met without needing a middleman. <br>
  - For Example: <br>
    Let’s say you want to buy a digital artwork. A smart contract can be set up so that as soon as you send the payment, the artwork is automatically transferred to you. No need for a 
    third party like PayPal or a bank.
  - Smart contracts use cases are ever growing. They can be even used for something as simple as a pair of friends making a bet on which team will win a sports game.
   - Why Are They Important? <br>
     - No Middlemen → No banks, lawyers, or companies needed to enforce the contract
     - Transparent → Everyone can see how the contract works (no hidden rules)
     - Secure & Immutable → Once written on the blockchain, it can’t be changed or tampered with
  <br>
- __Risk Tag__: Think of risk tags like warning labels on food—they alert you to potential dangers before you interact with a wallet or contract. These risk tags are provided by Webacy, a company that provides a security platform that helps protect crypto and NFT assets. There are a total of 32 risk_tags that we will be using. Each risk tag represents a different type of risk.
  - What do they detect?
    - Risks of a contract taking your funds through scam, hacks, or fraud
    - Hacking of your tokens
    - Suspicious activity such as involvement in shady transactions
    - Fake contracts mimicking legit ones

<h2> Step 1: Import the necassary libraries and load the dataset </h2>

__The libraries__: <br>
<br>
  &nbsp;&nbsp;&nbsp;&nbsp; - Pandas <br>
  &nbsp;&nbsp;&nbsp;&nbsp; - Numpy <br>
  &nbsp;&nbsp;&nbsp;&nbsp; - Matplotlib <br>
  &nbsp;&nbsp;&nbsp;&nbsp; - Seaborn <br>
  &nbsp;&nbsp;&nbsp;&nbsp; - Scipy <br>
  <br>

The dataset you will be using is a "__compiled_risk_dataset__". What exactly is in this dataset? This dataset contains 1094 entries of smart contract vulnerabilties. The first 3 columns contain essential information about the smart contract: the project name, the smart contract address, and the chain. The remaining columns are 32 potential risk tags that may be present in any given smart contract. The dataset is essentially a table that lists what specific risks are present in each contract.<br>
<br>
Download the dataset and save it into a pandas dataframe. Print the first five rive using the __.head()__ function and ensure it matches the following:
<br>

![image alt](https://github.com/DRehan003/Cluster_Analysis_of_Smart_Contract_Risks/blob/c30e9d17d21335726bc82239cfc9690e521009fe/Checkpoint_Images/Dataset_first_5_rows.png)
<br>
<h2> Step 2: Perform Feature Selection </h2>

Feature selection is the process of selecting the most important variables from your dataset that contribute the most to the predictive power of your model. This helps improve the model’s performance, reduce complexity, and speed up training. <br>
<br>
I chose 3 risks tags:
- __hidden_owner__: Indicates the true owner of the smart contract. Making the owner public ensures transparency between the owner and customer/client. <br>
- __Is_honeypot__: Type of deceptive contract designed to lure users into sending funds or interacting with it, only to discover that they cannot withdraw or access their funds later. <br>
- __exploitation__: Where vulnerabilities or flaws in a smart contract are taken advantage of by malicious actors to perform actions that were not intended by the contract's creators. These include unauthorized access, stealing funds, altering contract behavior, or manipulating data.  <br>

<br>
I chose these 3 risk tags since they encompass broad, yet important, domains of security in smart contracts. <br>
<br>
Use the following line of code to convert all the True and False values into binary form: <br>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; __selected_features = data_new[[feature_1,feature_2,feature_3]].replace({True:1, False:0})__

<h2> Step 3: Compute the Jaccard Distance </h2>

The Jaccard Distance is a metric used to compare the similarity and diversity of two sets. In cluster analysis, Jaccard distance is a useful measure when you are working with data that can be represented as sets or binary attributes. It helps in determining the dissimilarity between data points.<br>
<br>
Use the following code to compute the jaccard distance: <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; __from scipy.spatial.distance import pdist, squareform__ <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; __distance_matrix = pdist(selected_features, 'jaccard')__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __distance_square_matrix = squareform(distance_matrix)__ <br>
<br>
<h2> Step 4: Perform Clustering </h2>

Cluster analysis is a way to group things that are similar to each other. It is a form of unsupervised machine learning. Imagine you have a collection of items, and you want to sort them into groups based on their characteristics. Cluster analysis helps you automatically find these groups, or clusters, without needing to tell the computer exactly what the groups are in advance. <br>
<br>
Use the following code to perform clustering: <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp; __import scipy.cluster.hierarchy as sch__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __linkage_matrix = sch.linkage(distance_matrix, method='ward')__ <br>
<br>
<h2> Step 5: Plot A Dendogram </h2>

Now it is time to visualize our analysis. Use the following code to plot the dendogram: <br>

&nbsp;&nbsp;&nbsp;&nbsp; __plt.figure(figsize=(10, 7))__ <br> 
&nbsp;&nbsp;&nbsp;&nbsp; __dendrogram = sch.dendrogram(linkage_matrix)__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.title('Hierarchical Clustering Dendrogram')__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.xlabel('Data points')__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.ylabel('Jaccard distance')__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.show()__ <br>

If you selected the same features as me in your feature selection, your dendogram should look like this:
![image alt](https://github.com/DRehan003/Cluster-Analysis-of-Smart-Contract-Vulnerabilities/blob/6c9775f9ae67709e87abf8a6b579e49ebbac9508/Checkpoint_Images/Dendogram.png)

<br>
However, if you selected different features or less/more than 3 features, your dendogram can look very different. <br>
<br>
For example, as an experiment I went back and changed the feature selection on my analysis. Not only did I select completely different features, but I went from 3 features to 7. <br>
<br>
The features I selected were: <br>
&nbsp;&nbsp;&nbsp;&nbsp; - exploitation <br>
&nbsp;&nbsp;&nbsp;&nbsp; - bad_contract <br>
&nbsp;&nbsp;&nbsp;&nbsp; - external_dependencies <br>
&nbsp;&nbsp;&nbsp;&nbsp; - centralized_risk_medium <br>
&nbsp;&nbsp;&nbsp;&nbsp; - encode_packed_parameters <br>
&nbsp;&nbsp;&nbsp;&nbsp; - can_take_back_ownership <br>
&nbsp;&nbsp;&nbsp;&nbsp; - owner_change_balance <br>
<br>
The outcome of this dendogram is as shown below:
<br>

![image alt](https://github.com/DRehan003/Cluster-Analysis-of-Smart-Contract-Vulnerabilities/blob/5e9715851b459237de29de864b9c06d9d5f9a2b2/Checkpoint_Images/Dendogram_2.png)

What does the dendrogram show us? <br>
<br>
A Dendogram is a tree-like diagram that shows the hierarchical relationships between data points. It visually represents how clusters are merged or split based on similarity or distance. The vertical axis typically shows the level of similarity (or distance) between clusters, while the horizontal axis represents the individual data points or clusters. The branches merge as the clusters become more similar, with shorter branches indicating higher similarity. By analyzing the dendrogram, you can determine the optimal number of clusters and see which items are closely related based on their features. <br>
<br>
We can learn a lot from the denogram, but lets use a different form of visualization that maybe more helpful.

<h2> Step 6: Plot A Heat Map </h2>

Additionally, you can create a heat map as an alternative way to visualize the analysis. Use the following code to plot the heatmap:

&nbsp;&nbsp;&nbsp;&nbsp; __cluster_centers = data_new[[feature_1, feature_2, feature_3,'cluster']].groupby('cluster').mean()__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.figure(figsize=(12, 8))__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __sns.heatmap(cluster_centers, annot=True, cmap='coolwarm')__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.title('Heatmap of Cluster Centroids')__ <br>
&nbsp;&nbsp;&nbsp;&nbsp; __plt.show()__ <br>

The heatmap for the original features selection will look like this:
![image alt](https://github.com/DRehan003/Cluster-Analysis-of-Smart-Contract-Vulnerabilities/blob/1bfbce09ed83cc3a0e28dc27a0eb55e020433d90/Checkpoint_Images/Heatmap.png)

The heatmap for the second features selection I perfomed will look like this:
![image alt](https://github.com/DRehan003/Cluster-Analysis-of-Smart-Contract-Vulnerabilities/blob/1bfbce09ed83cc3a0e28dc27a0eb55e020433d90/Checkpoint_Images/Heatmap_2.png)

The more warm (red) a sect in the heatmap is, the more of that particular risk tag is present. For example, in the second heatmap we can see that in cluster 6, 57% of the contracts have the centralized_risk_medium tag. Whereas in clusters 1-4, we can see the centralized_risk_medium tag is not present in any of them. <br>
<br>
What does the heatmap show us? <br>
- The risk level of each cluster grows from 1 through 7; 1 being the least risky. <br>

What are some more detailed insights we can take away? <br>
- Contracts in cluster 1 possess negligible or no vulnerabilities <br>
- The can_take_back_ownership tag is particularly strong in cluster 7 <br>
- exploitation is particularly strong clusters 2 and 6, therefore must focus on minimizing their vulnerabilities from potential loss of funds <br>
- Contracts in clusters 4 and 5 must focus most on decreasing their  dependence on external systems and/or contracts <br>
- Contracts in clusters 6 and 7 need to be deepy reevaluated from top to bottom as they contain risks in all 7 selected features  <br>
- Contracts in cluster 6 are the most vulnerable for potential loss of funds out of all 7 clusters <br>

