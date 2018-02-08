# ORGanizer for Salesforce Javascript APIs

## Instructions

Include the `organizer-apis-x.x.x.min.js` file into your Visualforce page or Lightning component to get access to the ORGanizer APIs.

See the `example` folder.

## Usage

Use the `$ORGanizer` global variable to access the ORGanizer APIs.

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

*TBD*