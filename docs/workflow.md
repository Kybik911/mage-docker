# Workflow

The following guide shows you the normal development workflow using magedocker.

#### 1. Start containers

```
mage start
```
	
#### 2. Install/update dependecies with composer

```
mage composer <install/update>
```

#### 3. Develop code normally inside `magento/app`

While developing you might need to execute magento commands like `cache:flush` for example

```
mage magento <command>
```

#### 4. Working on frontend

```
mage grunt exec:<theme>
mage grunt watch
```

**NOTE:** You might also need to disable your browser cache. For example in Chrome:

* `Open inspector > Settings > Network > Disable cache (while DevTools is open)`

#### 5. Working on vendor modules [Mac only]

If you are developing code in a vendor module, you need to start unison watcher to sync files between host and container.

```
mage watch <magento_dir>/vendor/<vendor_name>/<module_name>
```

#### 6. xdebug

* Enable xdebug

	```
	mage debug-on
	```
		
* Configure xdebug in PHPStorm (Only first time)

	* [PHPStorm + Xdebug Setup](./xdebug_phpstorm.md)

* Sync generated **[Mac only]** 

	Because this folder is not binded for performance reasons, you need to sync it manually, so debugger finds the code in your host.

	```
	mage mirror-container generated
	```
		
	If you edit vendor files while debugging, you have to manually transfer the files into the container
		
	```
	mage mirror-host vendor/<subfolder_path>
	```
		
* Disable xdebug when finish 

	Environment is 10x slower when xdebug is enabled!

	```
	mage debug-off
	```
 
#### 7. Execute tests

* All tests

	```
	mage test-unit
	mage test-integration
	```
	
* Only specific files

	```
	mage test-unit <test-file-path>
	mage test-integration <test-file-path>
	```
