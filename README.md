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

The dataset you will be using is a "__compiled_risk_dataset__". What exactly is in this dataset? This dataset contains 1094 entries of smart contract vulnerabilties. The first 5 columns contain essential information about the smart contract: 
 <br>
 <br>
  &nbsp;&nbsp;&nbsp;&nbsp; - The project name	<br>
  &nbsp;&nbsp;&nbsp;&nbsp; - The smart contract address <br>
  &nbsp;&nbsp;&nbsp;&nbsp; - The blog post link	<br>
  &nbsp;&nbsp;&nbsp;&nbsp; - The audit website	<br>
  &nbsp;&nbsp;&nbsp;&nbsp; - The chain <br>
 <br>
The remaining columns are 32 potential risk tags that may be present in any given smart contract. The dataset is essentially a table that lists what specific risks are present in each contract.
<br>
<br>
Download the dataset and save it into a pandas dataframe. Print the first five rive using the __.head()__ function and ensure it matches the following:
<br>

![image alt](https://github.com/DRehan003/Cluster-Analysis-of-Smart-Contract-Vulnerabilities/blob/78dc0a333c94601251ce69c18702f9acc3cc1e25/Checkpoint_Images/Dataset_first_5_rows.png)
<br>
<h2> Step 2: Perform Feauture Selection </h2>
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

