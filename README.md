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
$ORGanizer.getVersion(function(version){
	//outputs 0.X.X.X
});
```

**isAwesome()**

Returns the extension version.

```javascript
$ORGanizer.isAwesome(function(version){
	//outputs 0.X.X.X
});
```