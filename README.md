
# auto_ssh_tools

This is a suit of tools written in shell for automatic ssh and scp, without entering passwords manually. To use the tools, you need to install expect.  

You can write a config file with only one line like this:

	192.168.0.122 root your_password 22

The first field  is the domain name or ip of your linux server. The second and third field are user name and password that you login with,  the last field is the port number that your ssh server listening on.

Save this file, for example i save it into `demo_ipfile/demo_machine`.

To do the automatic login, just goto the `auto_ssh_tool/` directory, and type the command:

	./goto demo_ipfile/demo_machine

Then you will find you've successfully logged into your server.

The `goto` script generates an expect script in `/tmp` with a random filename,  the it calls expect to execute the  expect script to complete the login.

Other tools in `auto_ssh_tool/` are implemented in the same way. 

If you just want to login to your server to execute a command and then exit, you can use `gotocmd` instead:

	 

-----

# automatic scp file transfer

If you need to pull file from your remote server or push local file to your remote server via scp, the `pullfile` and `pushfile` scripts will be useful.

To pull a file, use command like this:

	./pullfile demo_ipfile/demo_machine /root/test.txt /tmp

This 

	
	

