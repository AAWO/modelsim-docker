# Modelsim on Docker
ModelSim Version 16 GUI Running under docker container. Created for use with [VerilogDevEnv](https://github.com/AAWO/VerilogDevEnv).

## Build image
In order to build the image run the following command:
`docker build -t modelsim-docker <path-to-dockerfile>`

In case current working directory is this run:
`docker build -t modelsim-docker .`

## Steps for Linux
First you need to exec the `xauth list` on your host terminal. The aprox result will be:

`<hostname-of-machine>/unix: MIT-MAGIC-COOKIE-1 <some number here>`
  
Then exec `echo $DISPLAY`. The result will be **:1** or **:0**

Run the container with the following command:

`sudo docker run -i -t --name modelsim --net=host -e DISPLAY -v /tmp/.X11-unix -v <global-path-to-project-directory>:<gloval-path-to-mounted-directory-in-container> modelsim-docker bash`

Now inside the container exec the following command:

`xauth add <hostname-of-machine>/unix:<no-of-display> MIT-MAGIC-COOKIE-1 <some number here>`

Where the third arg is the result of `xauth list` command on your host and `<no-of-display>` is the **$DISPLAY** host machine value.

Finally exec `vsim` and enjoy. :)
