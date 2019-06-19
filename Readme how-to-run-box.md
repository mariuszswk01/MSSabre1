Run procedure for Windows

The following tools were used during the procedure testing:

-   Vagrant 2.1.1

-   VirtualBox 5.2.12

-   Windows 7 SP1

-   CygWin and PowerShell.

NOTE: All Vagrant commands must be run from the root directory of the project.

NOTE: You have to use the Vagrant release version 1.0.6; the details how to
download the mentioned release version are given below.

Follow the steps below to run the procedure:

-   upgrade Windows PowerShell, that is a part of the Windows Management
    Framework, to version 4.0 or higher. You can download the package from
    <https://www.microsoft.com/en-us/download/details.aspx?id=40855>. It is
    important to upgrade it because Vagrant will not work properly with previous
    versions of Windows PowerShell.

-   get the appropriate Vagrant installer from
    <https://www.vagrantup.com/downloads.html>, install the package and add it
    to the PATH system variable

-   install Nugrant plug-in to let users define .vagrantuser file at different
    locations. Set http_proxy and https_proxy environment variables to:

-   = export
    http_proxy=http://PROXY_USER:PROXY_PASSWORD_HERE\@proxy.server.com:80/

    = export
    https_proxy=http://PROXY_USER:PROXY_PASSWORD_HERE\@proxy.server.com:80/

    = vagrant plugin install nugrant

Please note that you need to encode all non alphanumeric characters (e.g. your
password) before exporting variables. If you have encoded string add it to the
PROXY_PASSWORD_HERE variable.

-   check out source files for the box-build Git project located at
    [git.server.com/box-run.git](git.server.com/box-run.git)

-   once both Vagrant and Nugrant are installed you can use Power Shell, Command
    prompt or sticky keys to start CygWin when working with Vagrant

-   edit the .vagrantuser file to specify the following data: CNTLM use (details
    below), limit of memory, CPUs assigned and whether additional software needs
    to be installed and whether to start GUI.

-   Please note that if you run the software for the first time or the global
    password has changed, export the environment variables: PROXY_USER and
    PROXY_PASS. This can be done only once as proper configuration file will be
    kept in the Virtual Machine (VM). You do not need to encode all non
    alphanumeric characters in the password but wrap the using the double
    quotes.

Make sure that all files in the project use the Unix style line endings before
running any command.

-   unset http_proxy and https_proxy environment variables

-   add a box(image) to Vagrant registry. Open terminal, browse to select the
    folder containing your project and run:

-   vagrant box add metadata.json

When the command is successfully finished you can verify if the image has been
added to Vagrant's registry; use the following command to check it:

vagrant box list

If you already have the image in the repository and would like to replace it
with a new one, remove the existing one first using the following command:

vagrant box remove centos-7-openshift.box

and then run the command that adds the image (see the above command for adding
image).

Please note that:

-   the Vagrant metadata.json file should be executed if there is no image in
    the local repository or there is a new version of the image that should
    replace the current version of the image.

-   you must have a private key located in:

-   = \~/.ssh/id_rsa if Cygwin is used

    = %USERPROFILE%\\.ssh if PowerShell or Command prompt is used

-   if you do not have a private key generated you can use PuTTYgen.exe to
    generate one. Please follow the instructions given here to generate the key:
    <https://www.ssh.com/ssh/putty/windows/puttygen>. It is worth mentioning
    that the private key should not be password-protected. When you have the key
    generated save it to %USERPROFILE%\\.ssh as the id_rsa variable. If you use
    CygWin copy the file to \~/.ssh.

Use the following commands to:

-   run the Virtual Machine (if the box is successfully deployed in Vagrant
    registry:

-   = vagrant up

-   give you access to a shell / box (if the Virtual Machine is up and running):

-   = vagrant ssh

-   stop working and shut down the running Virtual Machine:

-   = vagrant halt
