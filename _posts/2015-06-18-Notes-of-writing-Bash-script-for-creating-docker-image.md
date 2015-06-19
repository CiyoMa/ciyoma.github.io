---
layout: post
category: Script,Docker
tags: [Bash,Shell,Docker]
---
# Bash and a Bash example to create Docker image

#### Syntax

The script should begin with #!/bin/bash at the very top

##### create variable and assign value:

variable=value #do not put space near '=', if you want to modify the variable value, use the same syntax, do not write as $variable=value

after that you can use $variable to access the value of variable

##### ask input from user:

read [-p "prompt info"] variable

##### template for function:

	function f {
		#do something here
		#parameter can be accessed via $1,$2,$3... depends its position in the command
	}

##### template for if condition:

condition expr example (the spaces immediately after [ and before ] can not be ignored): 
[ $variable -eq 1 ]

	if [condition expr]; then
	  #do something if
	elif [condition expr]; then
	  #do something elif
	else
	  #do something else
	fi

##### template for while loop:

	while [condition expr]; do
	  #do something
	done

##### template for FOR loop:

	for i in `seq <#begin> <#end-exclusive>`; do
		#do something
	done

##### template for foreach loop:

	for i in $(ls) do
		#do something
		# $(ls) will create an anonymous variable storing all items that 'ls' command returns
	done

##### template for do while (until) loop:

	counter=20 #do not put space near '='
	until [condition expr]; do
	    #do something
	done

#### Named Pipe

Named Pipe is used for process communication.

mkfifo is used for making fifo named pipe (messages comes first will be sent out first)

When a process is reading the information in a pipe, the other process can not write into it.

If you redirect stdout to a named pipe, it may yield "broken pipe" error if the reader is
continuously checking if there is new content in the pipe.

#### Example

My last task in my internship at EMC is to write a Bash script that create docker image, installing some internal products and push it into a private docker registry.

But installing the products need to mount a NFS share containing all the code resources. At this moment (June 2015), "docker build" does not support to turn on the root privilege for mounting a NFS share inside container. Therefore writing a Bash script simulating human input is the only way for me to fulfill this task.

In the script I first run a docker container in background (put & in the end of the command line, so that it will run in another process, the main process won't wait it to finish.), redirect its stdin to a named pipe, then in the main process, echo commands for the running docker container into the named pipe.

In the script, the reason why I run the container in background is that the main process won't continue and issue commands into the running container.

For monitoring purpose, I also redirect the stdout of running container to a temporary file, the main process can check its output see when its end. (we can issue a echo command with some flag string into the running container. In the main process, when the flag appears in the output file, the running container has done its job) In this case, I tried named pipe as output destination as well, but it fails for the "broken pipe" issue I mentioned above.

You can get docker container via --cidfile option for docker run command or inside the running container issue "cat /proc/self/cgroup|grep -oP "docker/\K(.+)" |head -n1".

code sample:

	docker run -i -a=stdin -a=stdout -t=false --privileged --cidfile=/tmp/cid.txt repo:base /bin/bash </tmp/input_pipe >/tmp/output.txt &

	echo "mkdir -p /hello/world" > /tmp/input_pipe

	echo "cat /proc/self/cgroup|grep -oP \"docker/\\K(.+)\" |head -n1" > /tmp/input_pipe

	echo "echo end_of_process" > /tmp/input_pipe

	echo "exit" > /tmp/input_pipe

#code to check if end_of_process appears in /tmp/output.txt

#get container id from output.txt or cid.txt, do 
	
	imageID=$(docker commit $containerID $repoAndTag) 

#to get the imageID. Finally do 

	"docker tag $imagID dockerRegistryAddressAndPort/$repoAndTag" 
	"docker push dockerRegistryAddressAndPort/$repoAndTag"

