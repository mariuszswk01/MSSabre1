How to build Linux CentOS Virtual Machine with OpenShift for Vagrant

The following tools were used during the procedure testing:

-   Vagrant 2.0.2

-   VirtualBox 5.2.12

-   Windows 7 SP1

-   CygWin

NOTE: All commands must be run from the root directory of the project, unless
otherwise stated.

Use the following procedure to set up your Vagrant Virtual Machine:

-   download a suitable version of Packer for your operating system from
    <https://www.packer.io>, install the Packer and add the Packer to the PATH
    system variable

-   upgrade Windows PowerShell, that is a part of the Windows Management
    Framework, to version 4.0 or higher. You can download the package from
    <https://www.microsoft.com/en-us/download/details.aspx?id=40855>

-   check out source files for the box-build project located at
    [git.server.com/box-build.git](git.server.com/box-build.git)

-   open the centos-base-variables.json file and specify credentials for the
    proxy server. Please note that you need to encode all non alphanumeric
    characters

-   make sure that all files in the project use the Unix style line endings
    before running any command

-   open CygWin environment, change directory to the folder with your project
    and execute the additional steps:

    -   point ISO_URL= \#, a URL to the CentOS ISO containing the installation
        image or virtual hard; it has to be the DVD version available from
        <http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso>

    -   use the following build command to run the Packer build:
        -var-file=centos-base-variables.json -force centos-base.json

>   Note that when the packer build process is finished the centos-base.box file
>   is located in the current folder

-   edit the centos-openshift-variables.json file and specify a proxy username
    and a proxy password

-   make sure you have the correct version of VirtualBox installed; you should
    have version 5.2.12 installed on your disk; it is important because Guest
    Additions are propagated to the image from your local VirtualBox

-   open a terminal, browse to select the folder containing your project and run
    the Packer build -var-file=centos-openshift-variables.json -force
    centos-openshift.json

>   Note that when the packer build process is finished the
>   centos-7-openshift.box file should be located on your disk

-   upload the above mentioned file to maven.repository.com. Make sure that
    credentials are properly configured for a server with in your
    \~/.m2/settings.xml file (id set to user-upload) and run the following
    command:

>   mvn deploy:deploy-file -DgroupId=com.example \\

>   \-DartifactId=vagrant-centos-open-shift \\

>   \-Dversion=1.0.7 \\

>   \-Dpackaging=box \\

>   \-Dfile=centos-7-openshift.box \\

>   \-DrepositoryId=user-upload \\

>   \-Durl=http://maven.repository.com/content/repositories/releases

When the box is successfully uploaded:

-   create a Git Tag using the deployed version number: 1.0.X

-   update -Dversion command described above with 1.0.X+1 pattern to add the
    file to the repository
