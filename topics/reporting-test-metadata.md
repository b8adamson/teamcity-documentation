[//]: # (title: Reporting Test Metadata)
[//]: # (auxiliary-id: Reporting Test Metadata)

On this page:

<tag-list of="chapter" mode="tree" depth="5"/>

__Since TeamCity 2018.2__, a test run in TeamCity can be associated with some additional information (metadata), complementing test status, execution time, and output. This information can be used to provide extra logs, screenshots, numeric values, tags, and so on.   
You can now use service messages to report this kind of additional test data in TeamCity and then view it in the TeamCity Web UI.

## Reporting additional test data

Additional test data is reported using the `testMetadata` service message, with the following attributes:
* `name` (optional) is a name of the metadata item, used to distinguish different metadata items for the same test and to show this item in UI. When omitted, TeamCity autogenerates the name, but does not show it in UI.
* `testName` (optional) is the name of the test for which this metadata is generated, excluding the suite name. If the service message is reported in the middle of the test or immediately after its finish, the testName attribute can be skipped. If the metadata is reported later, it should contain the full test name, including suites, packages and so on.
* `value` (mandatory) contains the metadata value associated with the test. The max value length is 1024.
* `type` (optional) defaults to text unless otherwise specified. The type affects how metadata is stored and how its value is shown in the TeamCity UI.

If the format of the service message is incorrect, a corresponding note about it is written into build log.The types of data which can be recognised by TeamCity are as follows:

### Number


```Shell

##teamcity[testMetadata testName='package.Test.testName' name='setUp time' type='number' value='434.5']
```



You can see a graph of changes for a numeric value, from build to build for the given test.

### String/Text


```Shell
##teamcity[testMetadata testName='package.Test.testName' name='some key' value='a text'] 
```



### External links


```Shell
 ##teamcity[testMetadata testName='test.name' name='JetBrains' type='link' value='https://jetbrains.com']
```



### Links to build artifacts


```Shell
 ##teamcity[testMetadata testName='test.name' type='artifact' value='path/to/catalina.out']
```



The path to the artifact should be relative to the [build artifacts directory](build-artifact.md), and can reference a file inside archive:


```Shell
 ##teamcity[testMetadata testName='test.name' type='artifact' value='logs.zip!/testTyping/full-log.txt']
```



When showing links to artifacts, TeamCity shows both the `name` and the filename of the referenced image. If name was autogenerated, it is not shown.

### Image from artifacts directory


```Shell
##teamcity[testMetadata testName='test.name' type='image' value='path/to/screenshot.png']
```



The path to the image should be relative to the build artifacts directory. When showing images, TeamCity shows both the `name` and the filename of the referenced image.

## Displaying additional test data

You can view additional test data in various places in the TeamCity Web UI.

### Additional test data for a failed test

To view additional data for a test, expand the stacktrace: TeamCity shows it before test failure details in a separate Test Metadata section. 

<img src="add-test-data-failed-test.png" width="800px" alt="Additional test data for a failed test"/>

### Additional test data graph for numeric values

To view the test data graph, expand the stacktrace: TeamCity shows it before test failure details in a separate Test Metadata section.

<img src="add-test-data-num-val.png" width="800px" alt="Additional test data graph for numeric values"/>

### Additional data for successful tests

To view additional data for a successful test, go to the Tests tab or the Test History tab: the OK status for a test is now clickable if additional test data is present:


<img src="add-test-data-success.png" width="800px" alt="Additional data for successful tests"/>
