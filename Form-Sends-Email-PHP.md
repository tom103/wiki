# Contact Form / Sends Email with PHP

Items needed:

 * Text editor that supports HTML, CSS, and PHP. (Notepad++ is a great source!!)
 * [Vagrant](https://github.com/FreeCodeCamp/wiki/blob/master/Vagrant-Up.md) (We'll use Scotch-Box)

Step 1:

First, let's open GIT GUI and create a new repository. Make a new folder on whatever drive you use and name it emailform. Now under Repository on GIT GUI, you'll find an option "Git Bash". That will open a command line so we can add Scotch-Box to our repository. Follow the rest of the instructions under the [Vagrant](https://github.com/FreeCodeCamp/wiki/blob/master/Vagrant-Up.md) form to install the Vagrant box and finish the installment. It might take a few minutes in order for it to create the vagrant files. 

Next, start up Notepad++ or whatever text editor you'll be using. We'll be using Notepad++ in this example. Open two fresh files and save one as "index.php" and the other as "send_email.php" and save both to the directory where the Vagrant files are. The Scotch Box will have it's own "index.php" for it's landing page, so feel free to just overwrite and save our code there or delete one once you make sure it's the landing page for Scotch Box. Below you will find the code for both php files, the first being for the "index.php" and the last for the "send_email.php" file.

```
<!DOCTYPE html>
<html lang="en">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=1.0" />

<head>
    <meta charset="UTF-8">
    <title>Form that will take info and send Email</title>
</head>

<body>
<div>
                    <form class="" method="post" action="send_email.php">
                        First name:<br>
                        <input id="first_name" type="text" name="first_name"><br>
                        Last name:<br>
                        <input id="last_name" type="text" name="last_name"><br>
                        Phone:<br>
                        <input id="telephone" type="text" name="telephone"><br>
                        Email:<br>
                        <input id="email" type="email" name="email"><br>
                        Comment:<br>

                        <textarea name="message" cols="21" rows="4" style="resize: none"></textarea> <br><br>
                        <input class="form_submit" type="submit" name="submit" value="Submit">
                        <input class="form_reset" type="reset" name="reset" value="Reset">
                    </form>
</div>
</body>
<footer>
</footer>
</html>

```

```
<?php

session_start();

if(isset($_POST['submit'])) {
    $to = "youremail@somedomain.com"; // this is your Email address
    $from = $_POST['email']; // this is the sender's Email address
    $first_name = $_POST['first_name'];
    $last_name = $_POST['last_name'];
    $email = $_POST['email'];
    $telephone = $_POST['telephone'];
    $comments = $_POST['message'];
    $subject = "Contact Form";

    // PREPARE THE BODY OF THE MESSAGE

    $message = '<html><body style="background: #3f3f3f;">';
    $message .= '<table rules="all" style="border-color: #3f3f3f;" cellpadding="10">';
    $message .= "<tr style='color: #eee;'><td><strong>First Name:</strong> </td><td>" . strip_tags($_POST['first_name']) . "</td></tr>";
    $message .= "<tr style ='color: #eee;'><td><strong>Last Name:</strong> </td><td>" . strip_tags($_POST['last_name']) . "</td></tr>";
    $message .= "<tr style='color: #eee;'><td><strong>Email:</strong> </td><td>" . strip_tags($_POST['email']) . "</td></tr>";
    $message .= "<tr style='color: #eee;'><td><strong>Phone:</strong> </td><td>" . strip_tags($_POST['telephone']) . "</td></tr>";
    $message .= "<tr style='color: #eee;'><td><strong>Message:</strong> </td><td>" . $_POST['message'] . "</td></tr>";
    $message .= "</table>";
    $message .= "</body></html>";

    $headers = "From:" . $from;
    mail($to, $subject, $message, $headers);
    header('Location: index.php');


}


?>
```



Don't freak out, I know you're seeing HTML and PHP written in various locations, but this will work fine. The server will display all the HTML and the PHP will be performed on the server side. Remember, PHP is a server side scripting language.

Now, we need to turn Scotch Box's email catcher on, so go back to the command line when you selected "Git Bash" earlier. After each line, make sure to hit enter so the command line knows what you want done.
```
vagrant ssh
```
```
mailcatcher --http-ip=0.0.0.0
```
You will see some text on the screen sayin that the mailcatcher is now on. Then use the same IP address to see your page and you'll see a page that has an email feel to it. This is where all of your test emails will go to. If you don't tell Mailcatcher to turn on, then this IP address will tell you it's not working, so don't forget to SSH and turn on Mailcatcher.

Then visit: http://192.168.33.10:1080



Let's look at a few things on the "index.php" page in the browser (remember that you have to visit http://192.168.33.10 in order to see your page). First, you'll notice we have a form. That form consists of a first name, last name, telephone number, email, and a comment section. They have style with them in the "send_email.php" that you will see in the email. You can always assign a class and or 'id' to the sections of the form to style it, but you will learn that in Free Code Camps coursework. 

For simplicity, all fields are 'text' minus the comment area. I've included the "style" in order to stretch the comment area to resemble a larger text area. 

Keeping things simple, we've "name"d the text areas to match the PHP "send_email.php" file's calls so we don't get mixed up. Always remember your naming conventions, they will make life easy for you. 

In the HTML form, you'll see a "method" and it's equal to "POST". POST submits the data to be processed. Next, you see an "action" that is equal to "send_email.php" which tells the form that POST will do what is in the "send_email.php" file. 

In the "send_email.php" file you can do an assortment of actions such as validating an email address and many other cool things, but for simplicity, we'll keep it to the point and send an email with the information provided. The "style" inside the "send_email" are what you will see in the email received. 

At the top, there is a $to variable that will be your email address. As we are using Vagrant, you won't actually receive an email at your email address, but the Mailcatcher will. Once this is deployed to a live environment that is connected to the internet and not a virtual one you are creating and using on your local computer, only then would you receive the email. 

You'll notice "strip_tags" inside the "send_email.php" file, those strip the HTML tags from the information. The "session_start" starts the session for the POSTs. At the bottom, you'll see a "header('Location: index.php');" which will keep the page on that page instead of opening a new page. The form will clear on send so that the user knows the information has been sent and allows them to send another if they choose to do so. 

Now we check the Mailcatcher, http://192.168.33.10:1080 and we can see the messages we sent. You'll notice the styling from the style in the "send_email.php" file in the table format. 
