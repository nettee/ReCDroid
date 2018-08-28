# ReCDroid

The ReCDRoid is an android project to reproduce android bugs from bug report.

## 1. Usage:
### (1) Find all crashes. ReCDRoid tends to continually find other crashes after it triggers one.
`Input`: An android bug report and related apk.

`Exploration`: Using NLP to process bug report and BFS to seach crashs.

`Output`: All test cases which can trigger crash.

### (2) Find specific crash. ReCDRoid stops when it has triggered a specific crash which matchs the provided error message.
`Input`: An android bug report, related apk, related error message.

`Exploration`: Using NLP to process bug report and DFS to seach the specifc crash.

`Output`: A test case which can trigger crash with the input error message.

ReCDRoid can run test cases of output.

## 2. Example:
A bug report in https://github.com/milesmcc/LibreNews-Android/issues/22 as fellow:

- Install v1.4 from FDroid.
- Launch app.
- Disable automatically refresh
- Change server address to an invalid one, e.g., xxyyzz.
- Click refresh.



### (1)Example video:

`Exploration video`: example1-exploration.mkv

Youtube link: https://youtu.be/i0fQ58aUPa8

`Reproduce video`: example2-runTestCase.mkv

Youtube link: https://youtu.be/WVtp-Ld4WF0

### (2)Output test cases:
Output steps in run.xml: 

```
<step id="1"><currentClass>1</currentClass><subId>1</subId>...</step>
 
<step id="2"><currentClass>2</currentClass><subId>5</subId>...</step>

<step id="3"><currentClass>3</currentClass><subId>4</subId>...</step>

<step id="4"><currentClass>4</currentClass><subID>1</subID>...</step>

<step id="5"><currentClass>4</currentClass><subId>3</subId>...</step>

<step id="6"><currentClass>3</currentClass><subId>1</subId>...</step>
```

There are 6 steps for ReCDroid to trigger a bug. CurrentClass here is a page in android app. The detailed information of a papge can be found in the record.xml file with (CurrentClass in run.xml)=(ID in record.xml). I am apologize for the name disunion. It will be updated in the next version. Every papge has some UI components, so the subID is the compontent ID in this page. The detailed information of UI compoents can also be found in the record.xml with (subID in run.xml)=(runableID in record.xml). After subID, there are some detailed parameters as "..." to help tester knowing how to active this step.

### (3)Quick start example project
You needs 5 steps to run this project on your computer.

(1) Install android environment.

(2) Install gensim python environment.

(3) open an android avd with port 5554 and android 4.4.2

(4) download ReCDroid example project from Google file link(there is a 200MB word2vec library in it): https://drive.google.com/open?id=19iXoI_8QtQMKBheS8fHhABt7YCS3rayg

(5) run it with percerun_LibreNews.sh in it.
