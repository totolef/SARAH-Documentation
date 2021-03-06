# Dedicated page for SARAH v4

_work in progress_

## Getting Started

## FAQ

## Plugin Development

We'll see here the things that are different from SARAH v3.

### Global variables

Variables `SARAH`, `Config` and `Profile` are now globals. They are available anywhere in JavaScript code or EJS pages. 

The variable `SARAH` is a singleton that proxy all the API.
```javascript
  SARAH.speak('hello');
  SARAH.ConfigManager.save();
```
#### Debug

Functions `debug()`, `log()`, `info()`, `warn()`, `error()` are now globals.  They are available anywhere JavaScript. They can be called to log some information.

```javascript
  info('a trace %s accurate', 'very', { 'key' , 'value' });
```

#### Multilang

Function `i18n()` is now global and available anywhere in JavaScript code or EJS pages. It translate a lang key in correct language.

```javascript
  var message = i18n('portal.hello', 'John');
  info(message)
```

Localized files are stored in `server/app/locales/{lang}.js` and in `plugins/MonPlugin/locales/{lang}.js`.



### Differences with version 3

#### exports.action(data, next)

With v3, the function had **four** parameters: `exports.action(data, callback, config, SARAH)`.  
With v4, the function has **only two** parameters: `exports.action(data, next)`

From now on `config` is a global variable known as `Config`, and `SARAH` becomes also a global variable.

`callback` is now called `next`, but its role is identical.

### How To

#### How to update a {plugin}.prop variable

Variable defined in the `{plugin}.prop` can be edited in the portal. Update is saved in `custom.prop`. This action can also be performed in code:

```javascript
exports.action = function(data, next) {
  // Update in memory configuration
  Config.modules.{plugin}.myVariable = 123;
  
  // Save configuration (in custom.prop)
  SARAH.ConfigManager.save();
  
  next({'tts': "File saved"});
}
```
