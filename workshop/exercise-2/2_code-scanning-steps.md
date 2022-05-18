## Setup Code Scanning (using CodeQL)

```
Code scanning is a feature that you use to analyze the code in a GitHub repository 
to find security vulnerabilities and coding errors. 
```

In this section, we will go through
 1. how to setup a code-scannning workflow using CodeQL (there are other tools for code-scanning that can be used in GH workflows too)
 2. where to check vulnerabilites identified by the tool

### 1. Go to Security tab of your repo :
<img width="345" alt="image" src="https://user-images.githubusercontent.com/58063491/168086730-354d4ba3-97a9-482f-a047-f8b762f8adb8.png">

### 2. Click on 'Set up Code Scanning'
<img width="999" alt="image" src="https://user-images.githubusercontent.com/58063491/168086809-dd27b0e5-a34b-4eb7-9130-c8856de0cd10.png">

### 3. Click on 'Configure CodeQL alerts'
<img width="876" alt="image" src="https://user-images.githubusercontent.com/58063491/168086961-24db3d8f-10e3-4b99-a925-eb72b33aaedf.png">

### 4. Default workflow gets populated 
<img width="686" alt="image" src="https://user-images.githubusercontent.com/58063491/168087070-4b026678-49c9-4bad-8902-db52d94f63e3.png">

#### Points to note
  - when is it triggered - scheduled, or on push
  - languages of the repo - to decide which tool to use
  - Which branch is checkout - to ensure we scan the required branches

### 5. Commit and run

### 6. See scan results
To see the alerts and runs, we need to go to Security tab -> Code Scanning Alerts from the menu on the left.
<img width="411" alt="image" src="https://user-images.githubusercontent.com/58063491/169008628-b1b3eb1f-5f2c-455f-a67b-8c432b8963ba.png">


## 📚 Resources:
   - [Tools for code scanning - GH docs](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning#about-tools-for-code-scanning)
   - [Code scanning configs - GH docs](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/configuring-code-scanning)


## Exercise 2 : Step 2
[Next](./3_container-scan-steps.md)
