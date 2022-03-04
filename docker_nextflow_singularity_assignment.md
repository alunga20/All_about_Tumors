---
# Singularity Containers.

* Containers - help with reproducibility and dependancies required to run a script, program or pipeline.

## Initial Setup.

```bash
module load singularity
```

- To use the container on your local machine, you'll need to load the Singularity module.
- It's as simple as the command above.

## Finding and Downloading a Singularity Container.

* There are two main places that you can find containers that will work with singularity.

  . _https://singularity-hub.org/_
  
  . _https://hub.docker.com_
* The first time you use singularity it'll by default put a _.singularity_ folder in your home directory which commonly has a limited space.

_Example from Docker shub._

```bash
singularity pull docker://sjackman/maker
singularity exec --bind $PWD ./maker.img maker --help
```
_Example from Singularity hub_

_http://datasets.datalad.org/?dir=/shub_ use link to locate the container you want through the search box located in the site's page just below the *ADD A COLLECTION* button.

## Creating your own Singularity containers.
### 1. Building an image

* If working locally start a singularity VM

```bash
vagrant init singularityware/singularity-2.4
vagrant up
vagrant ssh
```

* Place the example recipe above into a file named recipe then create a singularity image  using the following command;
```bash
sudo singularity build test.simg recipe
```
## Singularity containers and GitHub Repos.

_Organization of the GitHub Repo_

* one of the goals is to share codes and scripts on GitHub. Containers take this to another level by providing all the prerequisites built into the script itself.

* The GitHub repo can be used in the traditional way where you git clone the repo and use the functions inside <utilities> or it can be used with the new method by calling singularity containers. 
  
```bash
git clone https://github.com/ISUGIFsingularity/utilities.git
cd utilities
ls
``` 
  
```
_output_  README.md  Singularity.1.0.0 utilities         wrappers
 ```

## Modifying Exsiting Containers
_Method 1_
```bash
sudo singularity build --writable file_name_1.simg file_name.simg
sudo singularity build --section environment file_name.simg ../recipe
```


* You can modify/update each section individually

_Method 2_
  
* You can also modify/install/update from within a container. For the environment, it is easier to do method 1 above.  
```bash
  more /environment
```
#### Custom environment shell code should follow.
  
 ```bash
SPACK_ROOT=/opt/spack
export SPACK_ROOT
export PATH=$SPACK_ROOT/bin:$PATH
source /etc/profile.d/modules.sh
source $SPACK_ROOT/share/spack/setup-env.sh
export PATH=$SPACK_ROOT/isugif/snpphylo/bin:$PATH
```  

## Building Over an existing image.

```bash
 sudo singularity build container.simg recipe
```  
* If you change something in a recipe you can just re-execute the build command and it will build only the changes you made in the recipe file.  
*  Once you have made all the changes and your image is working the way you want then you can make those changes in your original recipe file and recreate it from scratch for full reproducibility. 
  
  
# Running Nextflow on GitHub.
  
* Nextflow seamlessly integrates with GitHub, and GitLab hosted code repositories and sharing platforms.
* This feature allows you to manage your project code in a more consistent manner or use other people’s Nextflow pipelines, published through them.
  

### How it Works.
  
  * When you launch a script execution with Nextflow, it will look for a file with the pipeline name you’ve specified.
  
  * If that file does not exist, it looks for a public repository with the same name on GitHub. 
  
  * If found, the repository is automatically downloaded to your computer and executed. 

  * This repository is stored in the Nextflow home directory, that is by default the _$HOME/.nextflow_ path, and thus will be reused for any further executions.
 
  
1. You can run a project by specifying the project name as shown below, run the command:
  
```
nextflow run nextflow-io/hello -with-docker
```
  
2. Step 1 automatically downloads the container and stores it in the _$HOME/.nextflow folder_.

   - To check the project information, run the following command:
```
nextflow info nextflow-io/hello
```  

3. Any Git branch, tag or commit ID defined in a project repository, can be used to specify the revision that you want to execute when launching a pipeline by adding the _-r_ option to the run command line:

```
nextflow run nextflow-io/hello -r dev
```
- Revision are defined by using Git tags or branches defined in the project repository.This allows a precise control of the changes in your project files and dependencies over time.  
  
 4. The _clone_ command allows you to copy a Nextflow pipeline project to a directory of your choice. For example:
 ``` 
nextflow clone nextflow-io/hello target-dir  
```  
  
 5. Downloaded pipelines can be deleted by using the _drop_ command:
```
  nextflow drop nextflow-io/hello
```  
  
# Docker Hub
  
* Docker Hub is a service provided by Docker for finding and sharing container images with your team. 
  
* Docker Hub provides the following major features:

   - Repositories: Push and pull container images.
  
   - Teams & Organizations: Manage access to private repositories of container images.
  
   - Docker Official Images: Pull and use high-quality container images provided by Docker.
  
   - Docker Verified Publisher Images: Pull and use high- quality container images provided by external vendors.
  
   - Builds: Automatically build container images from GitHub and Bitbucket and push them to Docker Hub.
  
   - Webhooks: Trigger actions after a successful push to a repository to integrate Docker Hub with other services.

* Below is a step-by-step guide on how to get started with Docker Hub and Upload  your container image(Dockerfile) to Docker Hub:
  
## Step 1 (Downloading and Installing Docker Engine)
  
  - Download and install [Docker Desktop](https://docs.docker.com/desktop/#download-and-install) . If on Linux, download [Docker Engine](https://docs.docker.com/engine/install/).
  
 - Sign into the Docker Desktop applcation using the Docker ID created above.
  
## Step 2 (Building and Pushing a container Image to Docker Hub)
  - Start by creating a [Docker File](https://docs.docker.com/engine/reference/builder/) specify your application as below:
  
  ```bash
  FROM busybox
  CMD echo "Hello world! This Is My First Docker Image. "
  ```
  
  - To build your Docker image, run:  `docker build -t <your_username>/my-private-repo`
  
  - Run `docker run <your_username>/my-private-repo` to test your Docker image locally.
  
  - Run `docker push <your_username>/my-private-repo` to push your Docker image to Docker Hub. 
  
  - You should see a similar output:
  
  ![image](https://docs.docker.com/docker-hub/images/index-terminal.png)
  
  - Your Repo in Docker Hub should now display a new the recently uploaded image.
