# daemon

[![Build Status](https://secure.travis-ci.org/indexzero/daemon.node.png)](http://travis-ci.org/indexzero/daemon.node)

This is a fork of the [daemon](https://npmjs/package/daemon). It includes a few additional features with the current being only 1 feature in which a second argument (boolean) can be passed to the main imported function to indicate whether the newly created child process should be returned or if the main parent process should be killed (default).

## install via npm

```
npm install daemon-plus
```

Requires node >= 0.8

## examples

```javascript
// this code is run twice, once by the
// main process and once by the daemon
// see implementation notes below
console.log(process.pid);

require('daemon-plus')(); // creates new child process, exists the parent

// different pid because we are now forked
// original parent has exited
console.log(process.pid);
```

## api

### daemon(opt, returnChild)

Respawn the process (self) as a daemon. The parent process will exit at the point of this call.
`opt` parameter see below.
`returnChild` [Boolean] when true, the parent process won't be exited and instead the instantiated child process will be returned.

### daemon.daemon(script, args, opt)

Spawn the `script` with given `args` array as a daemonized process. Return the `child` process object.

opt can optionally contain the following arguments:
* stdout (file descriptor for stdout of the daemon)
* stderr (file descriptor for stderr of the daemon)
* env (environment for the daemon) (default: process.env)
* cwd (current working directory for daemonized script) (default: process.cwd)

## implementation notes

Daemon actually re-spawns the current application and runs it again. The only difference between the original and the fork is that the original will not execute past the `daemon()` call whereas the fork will.

## node versions prior to 0.8

Using this module on older versions of node (or older versions of this module) are not recommended due to how node works internally and the issues it can cause for daemons.

## Contributors
[Charlie Robbins](http://nodejitsu.com)  
[Pedro Teixeira](https://github.com/pgte)  
[James Halliday](https://github.com/substack)  
[Zak Taylor](https://github.com/dobl)  
[Daniel Bartlett](https://github.com/danbuk)  
[Charlie McConnell](https://github.com/AvianFlu)  
[Slashed](http://github.com/slashed)  
[Roman Shtylman](http://github.com/shtylman)  

