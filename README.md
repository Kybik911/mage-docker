# Magento 2 MageDocker

Plug and play Magento 2 dev environments with docker. **Fastest performance ever** on Mac and Linux.

## Performance Comparison

#### Up to 7x faster development experience on Mac compare to standard docker setups.

#### Check out all benchmarks

* [Benchmarks: MageDocker vs Standard Docker](docs/benchmarks.md)

#### Learn more about how that is achieved

* [Overcoming Docker for Mac performance issues](docs/overcome_performance_issues.md)

---

## What is MageDocker?

MageDocker is just a bash script ready to use in Linux and Mac to be able to use docker with best native performance.

While performance might no be a problem for Linux, using this tool is the only way you can overcome performance issues on Mac. MageDocker allows you to have different configuration for each system while using the same workflow. So your whole team can work the same way no matter which computer they are using. It just works!

## Supported Systems

* Mac
* Linux

---

## Video Tutorials

If you do not like reading and prefer watching videos. Check out all video tutorials here:

* [Video Tutorials](./docs/video_tutorials.md)

---

## Installation

You only need 3 things on your local machine: `git`, `docker` and `mage`

### Install Docker

Follow the installation steps for your system.

<details>
<summary>Mac</summary>
	
1. Install Docker on [Mac](https://docs.docker.com/docker-for-mac/install/)

2. Configure `File Sharing` settings for the folder that contains your projects

	![File Sharing Configuration](docs/img/file_sharing.png)
	
3. Optionally you can also apply these performance tweaks

	* [http://markshust.com/2018/01/30/performance-tuning-docker-mac](http://markshust.com/2018/01/30/performance-tuning-docker-mac)

</details>
	
<details>
<summary>Linux</summary>
	
1. Install docker

	* Install Docker on [Debian](https://docs.docker.com/engine/installation/linux/docker-ce/debian/)
	* Install Docker on [Ubuntu](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/)
	* Install Docker on [CentOS](https://docs.docker.com/engine/installation/linux/docker-ce/centos/)

2. Configure permissions
	
	* [Manage Docker as a non-root user](https://docs.docker.com/install/linux/linux-postinstall/)

</details>

### Install MageDocker console

1. Clone this repo

    ```
    git clone [https://github.com/RusDovOnilab/dockergento-upd.git](https://github.com/Kybik911/mage-docker.git)
    ```

2. Add `mage` bin into your `$PATH`

    ```
    sudo ln -s $(pwd)/mage-docker/bin/mage /usr/local/bin/
    ```
    
3. Open a new terminal tab/window and check that `mage` works

	```
	which mage
	mage
	```

</details>


## Project Setup

Depending the type of project, you can use one of the following setups:

### Dockerize existing project

```
cd <your_project>
mage setup
```

### New project

```
mkdir <new_project_name> && cd <new_project_name>
mage setup
mage create-project
```

### Magento 2 github for contribution
**Disclaimer:** Performance on Mac is slower here due to the huge amount of files in `app` (~20.000 files)

<details>
<summary>Workaround to improve performance on Mac</summary>
	
1. Remove these lines on `docker-compose.dev.mac.yml`
    
    ```
        - ./app:/var/www/html/app:delegated
        - ./dev:/var/www/html/dev:delegated
        - ./generated:/var/www/html/generated:delegated
        - ./pub:/var/www/html/pub:delegated
        - ./var:/var/www/html/var:delegated
    ```
 
2. Sync `app` using `unison` container. Add this in `docker-compose.dev.mac.yml`
     
    ```
    unison:
      volumes:
        - ./app:/sync/app
    ```

3. Mirror not synced folders before executing composer the first time

	```
	mage start
	mage mirror-host app dev generated pub var
	```

4. If you are editing code in `app`, you need to start unison watcher to sync files between host and container.

	```
	mage watch app/code/Magento/<module_name>
	```
    
</details>

```
git clone https://github.com/magento/magento2.git
cd magento2
mage setup
```

---

## Usage

### Start Application

```
mage start
mage composer install
sudo vim /etc/hosts
// Add -> 127.0.0.1 <your-domain>
```

Open `http://<your-domain>` in the browser 🎉

### Workflow

See detailed documentation about development workflow with MageDocker

* [Development Workflow](docs/workflow.md)

---

## More Documentation

* [Multi store configuration](docs/multi_store.md)
* [PHPStorm + Xdebug Setup](docs/xdebug_phpstorm.md)
* [Grumphp setup](docs/grumphp_setup.md)
* [Docker images list](docs/docker_images.md)
* [Other customizations](docs/customizations.md)

## Troubleshooting

* [Troubleshooting](docs/troubleshooting.md)

---

## ChangeLog

* [CHANGELOG.md](CHANGELOG.md)

## Developers

* [Ruslan Dovnar](https://github.com/Kybik911)
* Based on [Dockergento](https://github.com/ModestCoders/magento2-dockergento)

## Resources

This project has been possible thanks to the following resources:

* [docker-magento](https://github.com/markoshust/docker-magento) by [@markshust](https://twitter.com/markshust)
* [Getting Started with Docker for Magento](https://nomadmage.com/product/getting-started-with-docker-for-magento-2/) by [@mostlymagic](https://twitter.com/mostlymagic)
* [Docker Background Sync](https://github.com/cweagans/docker-bg-sync) by [@cweagans](https://twitter.com/cweagans)

## Licence

* [GNU General Public License, version 3 (GPLv3)](http://opensource.org/licenses/gpl-3.0)

## Copyright
(c) Kybik911
