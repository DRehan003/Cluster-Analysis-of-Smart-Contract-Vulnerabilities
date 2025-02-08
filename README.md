<h1> Cluster Analysis of Smart Contract Vulnerabilities </h1>

Objective: Perform and analyze cluster analysis on a dataset of smart contracts in Python to identify similar risk profiles through the use of the pandas, numpy, matplotlib, seaborn, and scipy libraries. The different types of risks will be categorized into 32 different types of risks. <br>
<br>
Essential Terminology:
- Smart Contract: A self-executing program  stored on blockchain that automatically carries out an agreement when certain conditions are met without needing a middleman. <br>
  - For Example: <br>
    Let’s say you want to buy a digital artwork. A smart contract can be set up so that as soon as you send the payment, the artwork is automatically transferred to you. No need for a 
    third party like PayPal or a bank.
   - Why Are They Important? <br>
     - No Middlemen → No banks, lawyers, or companies needed to enforce the contract.
     - Transparent → Everyone can see how the contract works (no hidden rules).
     - Secure & Immutable → Once written on the blockchain, it can’t be changed or tampered with.
  <br>
- Risk Tags: Think of Webacy risk tags like warning labels on food—they alert you to potential dangers before you interact with a wallet or contract.
  - What do they detect?
    - Risks of a contract taking all your funds through scam, hacks, or fraud
    - Hacking and full control over your tokens
    - Suspicious activity such as involvement in shady transactions
    - Fake contracts mimicking legit ones

<h2> Step 1: Import the necassary libraries and load the dataset </h2>
The libraries: <br>
<br>
  &nbsp;&nbsp;&nbsp;&nbsp - Pandas <br>
  &nbsp;&nbsp;&nbsp;&nbsp - Numpy <br>
  &nbsp;&nbsp;&nbsp;&nbsp - Matplotlib <br>
  &nbsp;&nbsp;&nbsp;&nbsp - Seaborn <br>
  &nbsp;&nbsp;&nbsp;&nbsp - Scipy <br>
<br>
The dataset you will be using is a "compiled_risk_dataset". What exactly is in this dataset? This dataset contains 1094 entries of smart contract vulnerabilties. The first 5 columns contain essential information about the smart contract: 
 <br>
 <br>
  &nbsp;&nbsp;&nbsp;&nbsp - the project name	<br>
  &nbsp;&nbsp;&nbsp;&nbsp - the smart contract address <br>
  &nbsp;&nbsp;&nbsp;&nbsp - the Blog post link	<br>
  &nbsp;&nbsp;&nbsp;&nbsp - the audit website	<br>
  &nbsp;&nbsp;&nbsp;&nbsp - the chain <br>
  <br>
The remaining columns are 32 potential risk tags that may be present in any given smart contract. The dataset is essentially a table that lists what specific risks are present in each contract.
<br>
<br>
Download the dataset and save it into a pandas dataframe. Print the first five rive using the .head() function and ensure it matches the following:
![First 5 rows of the dataset](Checkpoint_Images/Dataset_first_5_rows.png)
![Alt Text](Checkpoint_Images/Dataset_first_5_rows.png)


  
