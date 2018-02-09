# ORGanizer for Salesforce Javascript APIs

<img src="http://organizer.enree.co/img/logo2.png" data-canonical-src="http://organizer.enree.co/img/logo2.png" width="200" />

[**organizer.enree.co**](https://organizer.enree.co)

## Instructions

Include the `organizer-apis-x.x.x.min.js` file into your Visualforce page or Lightning component to get access to the ORGanizer APIs.

The `organizer-apis-stage-x.x.x.min.js` files are used for the **ORGanizer** stage version (contact organizer@enree.co to join the beta testers).

Use the `example` folder to see a practical example of a Visualforce page using the APIs.

## Usage

Use the `$ORGanizer` global object to access the ORGanizer APIs.

```javascript
//asks ORGanizer if it is awesome
$ORGanizer.isAwesome(function(result){
    console.log(result);
});

//logins to a given ORG
$ORGanizer.login('my@salesforce.user.me', 
	$ORGanizer.CONSTANTS.LOGIN_MODE.NEW_WINDOW, 
	'/apex/LandingPage', function(result){
    console.log(result);
});
```

## Docs

**getVersion()**

Returns the extension version.

```javascript
$ORGanizer.getVersion(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": "9999.6.5.16"
}
```

**login()**

Login using the **ORGanizer** logins list.

```javascript
var username = 'my@userna.me';
var loginMode = $ORGanizer.CONSTANTS.LOGIN_MODE.NEW_WINDOW; //supported: NEW_WINDOW | SAME_WINDOW | INCOGNITO
var landingPage = '/apex/LandingPage'; // optional
$ORGanizer.login(username, loginMode, landingPage, function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": true
}
```

**loginAs()**

Login as another user in the current ORG.

Only supports inner Salesforce users.

```javascript
var userId = '00512345678945';
var incognitoMode = true;
$ORGanizer.loginAs(username, incognitoMode, function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": true
}
```


**isAwesome()**

Funny method.

```javascript
$ORGanizer.isAwesome(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": true
}
```

**getOrgInfo()**

Get's current ORG's info: it inclues:

* icon color
* tab title
* UI domain
* API domain
* history links (quick links in @history mode)
* custom quick links (quick links in @links mode)
* links of home / developer console / setup
* current session id
* Salesforce API level used

```javascript
$ORGanizer.getOrgInfo(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": {
    "color": "#0040ff",
    "title": "ORGanizer ORG",
    "domain": "custom-dev-ed.my.salesforce.com",
    "domainAPI": "custom-dev-ed.my.salesforce.com",
    "historyLinks": [
      {
        "d": 1518186500320,
        "l": "test history",
        "p": "/apex/ORGanizerAPITestPage"
      }
    ],
    "links": {
      "home": "https://custom-dev-ed.my.salesforce.com/home/home.jsp",
      "devConsole": "https://custom-dev-ed.my.salesforce.com/_ui/common/apex/debug/ApexCSIPage",
      "setup": "https://custom-dev-ed.my.salesforce.com/setup/forcecomHomepage.apexp"
    },
    "quickLinks": [
      {
        "l": "test page",
        "p": "/apex/testpage",
        "isCustom": true
      }
    ],
    "sid": "XXXXXXX!YYYYYYYYYY",
    "apiLevel": "40.0"
  }
}
```

**getAPICounter()**

Returns the number of Salesforce API calls issued by **ORGanizer** since the `from` date (in `long` format).

```javascript
$ORGanizer.isAwesome(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": {
    "count": 1618,
    "from": 1517587241935
  }
}
```

**getVIQs()**

Returns the list of Very Import Queries (VIQs) from the Quick Console's Query plugin.

```javascript
$ORGanizer.getVIQs(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": {
    "queries": [
      {
        "id": "06764703998873873",
        "createdDate": 1488469707952,
        "name": "CustomField",
        "body": "Select Id, DeveloperName, NamespacePrefix, TableEnumOrId \nFrom CustomField WHERE NameSpacePrefix = null order by TableEnumOrId, developername",
        "lastModifiedDate": 1488469707952
      },
      {
        "id": "02958357453820868",
        "createdDate": 1488377309512,
        "name": "My new query",
        "body": "Select Id, Name, \n    (Select Id, CaseNumber From Cases Where IsClosed = false), \n    (Select Id,LastName, FirstName From Contacts)\n\t\t\t\tFrom Account Order By Name ASC\n\t\t\t\t",
        "lastModifiedDate": 1488377309512
      }
    ]
  }
}
```

**getVISSs()**

Returns the list of Very Import Scripts (VISs) from the Quick Console's Execute Anonymous plugin.

```javascript
$ORGanizer.getVISs(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": {
    "scripts": [
      {
        "id": "08470779610833823",
        "createdDate": 1487606607051,
        "name": "Debug Test 000",
        "body": "System.debug('Hello World!');",
        "lastModifiedDate": 1487606927859
      },
      {
        "id": "005907734750728055",
        "createdDate": 1518190532621,
        "name": "VIQ 2",
        "body": "List alist = [Select Id From Account];\naList[0].Name = 'First';\nupdate aList;",
        "lastModifiedDate": 1518190532621
      }
    ]
  }
}
```

**getLicense()**

Returns license type and main max quotas.

```javascript
$ORGanizer.getLicense(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": {
    "MAX_SF_ACCOUNTS": 100,
    "MAX_SF_SINCHED_ACCOUNTS": 50,
    "license": "BETA"
  }
}
```

**getLimits()**

Returns current **ORGanizer** storage limits.

Limits include:

* Total Sync quota % used
* Total Local quota % used
* Total Sync items (phisical limit)
* Total Sync accounts (license limit)
* Total Local Accounta (license limit)

```javascript
$ORGanizer.getLimits(function(rslt){});
```

*Response*:

```json
{
  "success": true,
  "result": {
    "totalSyncQuotaPercentage": 1,
    "totalSyncItems": {
      "total": 1,
      "max": 400
    },
    "totalSyncAccounts": {
      "max": 50,
      "total": 0
    },
    "totalLocalAccounts": {
      "total": 0,
      "max": 100
    },
    "totalLocalStoragePercentage": 0
  }
}
```

**executeAnonymous()**

Run an Apex script in execute anonymous.

```javascript
var script = "System.debug('Hello World!')";
var debugLevels = {
    'Db' : 'DEBUG',
    'Workflow' : 'DEBUG',
    'Validation' : 'DEBUG',
    'Callout' : 'DEBUG',
    'Apex_code' : 'DEBUG',
    'Apex_profiling' : 'DEBUG',
    'Visualforce' : 'DEBUG',
    'System' : 'DEBUG',
};
$ORGanizer.executeAnonymous(script, debugLevels, function(rslt){});
```

*Response*:

```json
 {
  "success": true,
  "result": {
    "result": {
      "column": "-1",
      "compileProblem": "",
      "compiled": "true",
      "exceptionMessage": "",
      "exceptionStackTrace": "",
      "line": "-1",
      "success": "true"
    },
    "debugLog": "40.0 APEX_CODE,DEBUG;APEX_PROFILING,DEBUG;CALLOUT,DEBUG;DB,DEBUG;SYSTEM,DEBUG;VALIDATION,DEBUG;VISUALFORCE,DEBUG;WORKFLOW,DEBUG\nExecute Anonymous: system.debug('test');\n16:53:20.33 (33981272)|USER_INFO|[EXTERNAL]|0050Y000000Dtt3|organizer@enree.co|Ora standard dell’Europa centrale|GMT+01:00\n16:53:20.33 (34008240)|EXECUTION_STARTED\n16:53:20.33 (34013848)|CODE_UNIT_STARTED|[EXTERNAL]|execute_anonymous_apex\n16:53:20.33 (34500383)|USER_DEBUG|[1]|DEBUG|test\n16:53:20.34 (34547628)|CUMULATIVE_LIMIT_USAGE\n16:53:20.34 (34547628)|LIMIT_USAGE_FOR_NS|(default)|\n  Number of SOQL queries: 0 out of 100\n  Number of query rows: 0 out of 50000\n  Number of SOSL queries: 0 out of 20\n  Number of DML statements: 0 out of 150\n  Number of DML rows: 0 out of 10000\n  Maximum CPU time: 0 out of 10000\n  Maximum heap size: 0 out of 6000000\n  Number of callouts: 0 out of 100\n  Number of Email Invocations: 0 out of 10\n  Number of future calls: 0 out of 50\n  Number of queueable jobs added to the queue: 0 out of 50\n  Number of Mobile Apex push calls: 0 out of 10\n\n16:53:20.34 (34547628)|CUMULATIVE_LIMIT_USAGE_END\n\n16:53:20.33 (34588939)|CODE_UNIT_FINISHED|execute_anonymous_apex\n16:53:20.33 (35446737)|EXECUTION_FINISHED\n"
  }
}
```
