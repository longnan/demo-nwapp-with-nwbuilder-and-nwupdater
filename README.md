# Demo-nwapp with nwbuilder and nwupdater
> Node-Webkit Demo of how to use nw-builder and nw-updater, based on example from:
- https://github.com/nwjs/nw-builder/tree/master/example/ 
- https://github.com/edjafarov/node-webkit-updater/tree/master/app

### nw-builder:
https://github.com/nwjs/nw-builder

### node-webkit-updater:
https://github.com/edjafarov/node-webkit-updater

### Changes:
#### updater.js
```javascript
      function deleteApp(cb){
		  console.log("del:" + to);
		  // In windows platform, can't delete nw parenet running folder 'to' AppPath, just to delete all content inside AppPath
		  //del(to, {force: true}, cb);
		  del(to + '\\*', {force: true}, cb);        
      }
```	  

#### index.html
```javascript
    function newAppInstalled(err){
      if(err){
        console.log(err);
        return;
      }
	  // Can't pass null to upd.run, should use [] as parameter
	  //upd.run(execPath, null);	 
      upd.run(execPath, []);	  
      gui.App.quit();
    }	  
```

### Build & Install
#### Install nw-builder (run as Administrator in Windows Platform)
```shell
npm install nw-builder -g
```

#### Install node_modules dependency for demo nwapp
```shell
cd nwapp
npm install
```

### Install node_modules dependency for demo builder (optional if you don't have all modules for nw-builder yet)
```shell
# goto root of demo
npm install
```

#### Build & Packaging demo nwapp (run as Adminstrator in Windows Platform)
```shell
# goto root of demo
nwbuild -v 0.12.3 -p win64 ./nwapp
```

#### Zip nwapp
Make <b>nwapp.zip</b> for including all contents under build\nw-demo\win64\ 
Copy <b>nwapp.zip</b> to folder nw-demo-web

### Running Demo nwapp
Copy folder nw-demo-web to web server (eg. Tomcat Webapp)
Run nwapp 
```shell
build\nw-demo\win64\nw-demo.exe
```
No update, running version is latest version if it compare to latest.json in nw-demo-web

### Test Demo nwapp updater
Change latest.json for testing purpose, no actual version upgrade in nwapp.zip :
"version": "0.1.0" -> "version": "0.1.1"

Then try to Run nwapp, nwapp updater is working now. Enjoy! :-)
