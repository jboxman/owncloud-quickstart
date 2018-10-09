# Getting started with ownCloud

With [ownCloud](https://owncloud.org/) your data is accessible from anywhere on
your computer, tablet, or mobile phone. ownCloud runs on and stores your data on
servers you manage.

This guide discusses the following topics:

* [Installing and configuring ownCloud](#installing-and-configuring-owncloud)
* [Allowing access on port 8080](#allowing-access-on-port-8080)
* [Adding a user account](#adding-a-user-account)
* [Connecting to ownCloud with a desktop or mobile phone](#connecting-to-owncloud-with-a-desktop-or-mobile-phone)

## Installing and configuring ownCloud

You can install ownCloud with [Docker Compose][compose]. You must have [Docker
installed][docker] on the computer you intend to run ownCloud on. To install and
configure your ownCloud server, read [Installing with Docker][installing].

## Allowing access on port 8080

By default, ownCloud listens on port `80` and port `443`. Complete the following
steps to configure ownCloud to listen on a different port.

1.  Change to the directory where the `.env` file you created in [Installing and
    configuring ownCloud](#installing-and-configuring-owncloud) exists.
1.  Execute the following command to change the HTTPS port to `8080`:

    ```bash
    $ sed -i 's/^HTTPS_PORT=.*$/HTTPS_PORT=8080/' .env
    ```

1.  Stop your ownCloud instance by executing `docker-compose down`:

    ```
    $ docker-compose down
    Stopping docker_owncloud_1 ... done
    Stopping docker_redis_1    ... done
    Stopping docker_db_1       ... done
    Removing docker_owncloud_1 ... done
    Removing docker_redis_1    ... done
    Removing docker_db_1       ... done
    Removing network docker_default
    ```

1.  Start your ownCloud instance by executing `docker-compose up -d`:

    ```
    $ docker-compose up -d
    Creating network "docker_default" with the default driver
    Creating docker_db_1    ... done
    Creating docker_redis_1 ... done
    Creating docker_owncloud_1 ... done
    ```

1.  To confirm ownCloud is listening on port `8080` execute: `docker-compose ps`:

    ```
    $ docker-compose ps
        Name                     Command                  State                         Ports
    -------------------------------------------------------------------------------------------------------------
    docker_db_1         /usr/bin/entrypoint /bin/s ...   Up (healthy)   3306/tcp
    docker_owncloud_1   /usr/bin/entrypoint /usr/b ...   Up (healthy)   0.0.0.0:8080->443/tcp, 0.0.0.0:80->80/tcp
    docker_redis_1      /usr/bin/entrypoint /bin/s ...   Up (healthy)   6379/tcp
    ```

Your ownCloud instance will be accessible on port `8080`.

## Adding a user account

To add a new [standard user][user] account, complete the following steps:

1.  On your computer, go to `https://<server>/`. Replace `server` with the
    domain name or IP address of your ownCloud server.
1.  Enter your ownCloud username and password, and then click the **right
    arrow** icon to sign in.
1.  In the upper-right corner of the page, click your username, and then click
    **Users**.
1.  At the top of the page, enter the following information:
    - In the **Username** field, enter a username
    - In the **E-Mail** field, enter an email address for the user
    - (Optional) Click the **Groups** list and select one or more groups to add
      the user to
1.  Click **Create**.

ownCloud will send an email to the user's email address with an activation link
to set the account password. If you want to a user to have group admin or super
admin capability, read [Granting Administrator Privileges to a User][admin].

## Connecting to ownCloud with a desktop or mobile phone

You can connect to ownCloud from your computer, a tablet, or mobile phone.

### Connecting to ownCloud with a desktop computer

The ownCloud client runs on Microsoft Windows, OS X, and Linux. To connect to
ownCloud from your computer, complete the following steps:

1.  From your computer, visit <https://owncloud.com/download/> and download the
    version for your operating system.
1.  After the download finishes, run the installer to start the ownCloud
    Connection Wizard.
1.  In the **Server Address** field, enter the URL for your ownCloud server. For
    example, `https://<server>/`. Replace `server` with your ownCloud domain
    name or IP address.
1.  Click **Next**. If you are using a self-signed TLS certificate, the
    **Untrusted Certificate** window is displayed. Click **Trust this
    certificate anyway** and click **OK**.
1.  Enter values for the following fields:
    - **Username**: Your oneCloud username
    - **Password**: Your password
1.  Click **Next**.
1.  Click **Connect**. ownCloud will begin synchronizing your files and
    directories.

To learn more about using the client on your computer, read [Using the
Synchronization Client][desktop].

### Connecting to ownCloud with a mobile device

To connect from ownCloud from your tablet or mobile phone, complete the
following steps:

1.  From your computer, visit <https://owncloud.com/download/> and scan the QR
    code with the device you want to install the ownCloud app on. Or you can
    visit the app store for your device and install the ownCloud app from there.
1.  Open the ownCloud app on your device.
1.  Enter values for the following fields:
    - **Server Address**: URL for your ownCloud server. For example,
      `https://<server>/`. Replace `server` with your ownCloud domain name or IP
      address.
    - **Username**: Your oneCloud username
    - **Password**: Your password
1.  Tap **Connect**. If you are using a self-signed TLS certificate, you may be
    asked to trust the certificate.

To learn more about the mobile app, read the documentation for your mobile
device:

- [Using the ownCloud Android App][android]
- [Using the ownCloud iOS App][iphone]

[docker]: https://www.docker.com/get-started
[compose]: https://docs.docker.com/compose/
[installing]: https://doc.owncloud.org/server/10.0/admin_manual/installation/docker/#installation-on-a-local-machine
[user]: https://doc.owncloud.org/server/latest/admin_manual/configuration/user/user_roles.html#standard-user
[admin]: https://doc.owncloud.org/server/latest/admin_manual/configuration/user/user_configuration.html#granting-administrator-privileges-to-a-user
[desktop]: https://doc.owncloud.org/desktop/latest/navigating.html
[android]: https://doc.owncloud.org/android/android_app.html
[iphone]: https://doc.owncloud.org/ios/ios_app.html
