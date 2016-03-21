Check out the following links and install each program. Be sure that it matches your OS (Operating System).

https://www.virtualbox.org/

https://www.vagrantup.com/downloads.html

https://git-scm.com/downloads

Now that we have the necessary programs installed, let’s get down to business.

Git has several different programs we can use here. Let’s open the <b>Git GUI</b>. We also can start up <b>Virtual Box</b> so that we can see the box running.

Once you run the Git GUI, you’ll see several options. Let’s select the top option, <b>“Create New Repository”</b>.

Select the <b>“Browse”</b> button and select the drive you want to install and run your virtual machine / server from. You can right click in the folder area and create a new folder. Let’s name it <b>FreeCodeCampMachine</b>.

Now, you’ll see the Git Gui and beside Directory, you should see <b>C:/FreeCodeCampMachine</b>.

At the bottom, select the button that says <b>“Create”</b>.

Now the interface looks different. Don’t worry about any of the buttons at the bottom or freak out about all the options at the top. We want to work on one thing. Select the option at the top left that says <b>“Repository”</b>, then under that option, you’ll find <b>“Git Bash”</b>. Select <b>Git Bash</b>.

Now we see we are in a terminal / console window. You should see the name of your computer followed by <b>MINGW64 /d/FreeCodeCampMachine (master)</b>. That simply says we are operating in the folder you created and you are on the master repository. Later we will create a branch but let’s worry about that later. 

Now, let’s throw some commands down and get the ball rolling. First type the following and hit Enter:

<b>git clone https://github.com/scotch-io/scotch-box myProject</b>

This will create a folder inside your directory named <b>“myProject”</b>. Next, let’s drill into that folder, so enter the following commands and hit enter:

<b>cd myProject</b>
Now we’re in the folder we want to be in. Now type the following on the command line and hit enter:

<b>vagrant up</b>


Once the installs are done and you see the command line ready for more commands, we want to ssh into vagrant. Enter the following commands and hit Enter:

<b>vagrant ssh</b>

You will see <b>SCOTCH BOX</b> on the terminal screen. Now we want to install <b>Apache</b> and <b>PHP</b>. Enter the following text and hit Enter:

<b>sudo apt-get install apache2 php5 php5-dev</b>

It will tell you how much space you will be using and how much you’ll have left. Don’t worry about that, just hit <b>‘y’</b> and let the install begin.

Once the install is complete, we need to update the software (it will tell you that you need to as well most likely). Enter the following command and hit Enter:

<b>sudo apt-get update</b>

Now we can exit SSH. Enter the following and hit Enter:

<b>exit</b>

Now, let’s open a browser window and enter the following IP address:

<b>http://192.168.33.10/</b>

You should see a landing page for Scotch Box telling you everything that is there and installed. Now, when you dig through the file you created earlier, you’ll find one that says <b>“public”</b>. Inside that folder you’ll see a file named <b>“index.php”</b> and that’s what you see for the landing page. You can edit that file with a text editor, save it, and refresh your browser to see your changes. 


