
# auto_ssh_tools

This is a suit of tools written in shell for automatic ssh and scp, without entering passwords manually. To use the tools, you need to install expect.  

You can write a config file with only one line like this:

	192.168.0.122 root your_password 22

The first field  is the domain name or ip of your linux server. The second and third fields are user name and password that you login with,  the last field is the port number that your ssh server listening on.

Save this file, for example I save it into `demo_ipfile/demo_machine`.

To do the automatic login, just goto the `auto_ssh_tool/` directory, and type the command:

	./goto demo_ipfile/demo_machine

Then you will find you've successfully logged into your server.

The `goto` script generates an expect script in `/tmp` with a random filename,  the it calls expect to execute the  expect script to complete the login.

Other tools in `auto_ssh_tool/` are implemented in the same way. 

If you just want to login to your server to execute a command and then exit, you can use `gotocmd` instead:

	 ./goto demo_ipfile/demo_machine 'ls -ltr'

-----

# automatic scp file transfer

If you need to pull file from your remote server or push local file to your remote server via scp, the `pullfile` and `pushfile` scripts will be useful.

To pull a file, use command like this:

	./pullfile demo_ipfile/demo_machine /root/file_to_pull.txt /tmp/

Then the `/root/file_to_pull.txt` on the remote server will be transfered to your local directory `/tmp` via scp.

To push a file, use command like this:

	./pushfile demo_ipfile/demo_machine /tmp/file_to_push.txt /root/

Then the `/tmp/file_to_push.txt` in your local `/tmp` directory will be transfered to the remote server into the `/root/` directory.
