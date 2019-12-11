# ***Docker Commands***

**Run Docker Image**

docker run -it --name containerName -p hostPort:exposedPort imageName:version

**Run Docker Image in detached mode**

docker run -it **-d** --name containerName -p hostPort:exposedPort imageName:version

**Run Docker Image with Volume Mount**

docker run -it --name containerName -p hostPort:exposedPort **-v localHostPath:containerPath** imageName:version

**Inspect a Container**

docker inspect containerName

**Inspect a Container**

  >***docker logs containerName*** to view the log
  ***docker logs -f containerName*** to monitor the log

**Share Volume of another container**

 > **Run First Container**
 docker run -it --name **FIRST** -p hostPort:exposedPort -v localHostPath:containerPath imageName:version

 > **Run Second Container with volume of first Container (Assuming Name of Container sharing Volume is first)**
 docker run -it --name **SECOND** -p hostPort:exposedPort **--volumes-from** FIRST imageName:version

**Copy Data to-from Docker Container to LocalHost**

>Run the Container
docker run -it --name containerName -p hostPort:exposedPort imageName:version

> create a file in container
docker exec containerName touch /file.txt

> copy file to localHost
docker **cp containerName:/file.txt** pathOnLocal

> copy file from local to container (assuming file name sampleFile.txt is present on local $PWD)
docker cp sampleFile.txt containerName:/root/sampleFile.txt
>>*Above command will copy local file to /root/ location on container*


# **Creating Your First Docker Images:**

 >A docker images always start from a base docker image. There are multiple type of docker image and alpine is most populer one among all.
  Most used command in Docker file are **FROM, COPY, ADD, RUN, EXPOSE, CMD** and  **ENTRYPOINT** .

  > **FROM:** should be the first line of docker file.
  **COPY/ADD:** to add a local file to image
  **RUN:** Run specific shell Commands
  **EXPOSE**



> #### **EXAMPLE:**
 Save Below if a file named DockerFile

    FROM ubuntu:14.04
    RUN apt-get update
    RUN apt-get install -y python-pip
    RUN apt-get clean all
    RUN pip install flask
    ADD hello.py /tmp/hello.py
    EXPOSE 5000
    CMD ["python","/tmp/hello.py"]

  1. Above image build will start will ubuntu:14.04 as base version.
  2. Update Repository Cache
  3. install Python and pip
  4. install flask
  5. Add or Copy hello.py from local to /tmp/ location in image
  6. Expose port 5000
  7. RUN python /tmp/hello.py command

  RUN*** docker build -t *SamplecontainerName* .*** to create a image with name *SamplecontainerName*

  You could also define volume and link in docker file.


  # ***Best Practice***

  1. Run a single process per container.
  2. Take Advantage of Container linking.
  3. If dealing with data containers such as mysql, always use mount volume option.
  4. If need to add multiple file from local directory, always use *.dockerignore* file.
  5. Prefer to use official image from docker hub instead of creating your image from scratch.
  6. combine RUN shell commands with **&&**
