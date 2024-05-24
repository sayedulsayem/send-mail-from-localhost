# Sending Email from Localhost in Windows (WAMP/ XAMPP/ Laragon)

## To send email from localhost using PHP on WAMP, XAMPP, or Laragon, follow these steps:

1. Download and Extract Sendmail
    1. Download [sendmail.zip](https://raw.githubusercontent.com/sayedulsayem/send-mail-from-localhost/master/sendmail.zip) for Windows and extract it. You will get a folder called `sendmail`.
    2. Place the `sendmail` folder into your server root folder. This could be `C:\wamp\` or `C:\wamp64\` or `C:\xampp\` or `C:\laragon\`, or a similar location.
2. Configure Sendmail
    1. Open the `sendmail.ini` file from the `sendmail` folder and update it as follows:
    ```ini
    smtp_server=smtp.gmail.com
    smtp_port=465
    smtp_ssl=auto
    default_domain=localhost
    error_logfile=error.log
    debug_logfile=debug.log
    auth_username=your-gmail-account@gmail.com
    auth_password=your-gmail-application-password ; Follow step 3 to get application password
    pop3_server=
    pop3_username=
    pop3_password=
    force_sender=
    force_recipient=
    hostname=localhost
    ```
3. Get Gmail Application Password
    1. Go to [Google Account](https://myaccount.google.com/) -> Security -> 2-Step Verification -> App passwords.
    2. Create an application password with your desired name. Copy and keep the application password safe as you won't be able to view it again. Note that you need to enable 2-Step Verification if it isn't already enabled.
4. Enable PHP Extensions
    1. Enable `php_openssl` and `php_sockets` from your PHP extensions. This can usually be done via the PHP settings in your `WAMP` or `XAMPP`, or `Laragon` control panel or from `php.ini` file.
5. Update `php.ini`
    1. Open your `php.ini` file and update the `sendmail_path` as follows:
    ```ini
    sendmail_path = "C:\wamp\sendmail\sendmail.exe -t -i"
    ; or
    sendmail_path = "C:\wamp64\sendmail\sendmail.exe -t -i"
    ; or
    sendmail_path = "C:\xampp\sendmail\sendmail.exe -t -i"
    ; or
    sendmail_path = "C:\laragon\sendmail\sendmail.exe -t -i"
    ```
6. Restart Your Server
    1. Restart your `WAMP` or `XAMPP` or `Laragon` server to apply the changes.
7. Create a PHP File to Send Email
    1. Create a PHP file (e.g., send_email.php) in your `www` or `htdocs` directory (or in a subdirectory).
    2. Add the following code to the file:
    ```php
    <?php
    $to       = 'receiving@mail.com';
    $subject  = 'My test email';
    $message  = 'Hi, this is a test message!';
    $headers  = 'From: your-gmail-account@gmail.com' . "\r\n" .
                'MIME-Version: 1.0' . "\r\n" .
                'Content-type: text/html; charset=utf-8';
    if(mail($to, $subject, $message, $headers))
        echo "Email sent";
    else
        echo "Email sending failed";
    ?>
    ```
    3. Update the $to and $headers variables to set the recipient and sender (“From” header). Save the file.
8. Test Sending Email
    1. Open your browser and navigate to the PHP file you created (e.g., http://localhost/send_email.php).
    2. If configured correctly, you should see a message indicating whether the email was sent successfully.

By following these steps, you can configure your local server to send emails using your Gmail account. Make sure to handle your Gmail application password securely.