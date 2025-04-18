# GitLab Install & Set up on Ubuntu
===========================================


### 1. Update Your System

```
sudo apt update
sudo apt upgrade
```

### 2. Install Dependencies

```
sudo apt install -y curl openssh-server ca-certificates
```

### 3. Install Postfix (Optional)

```
sudo apt install -y postfix
```

### 4. Download and Install GitLab

```
curl https://packages.gitlab.com/gpg.key | sudo apt-key add -
```

### 5. Add the GitLab repository

```
sudo sh -c 'echo "deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ $(lsb_release -c | awk "{print $2}") main" > /etc/apt/sources.list.d/gitlab_gitlab-ce.list'
```

### 6. Update the package list again

```
sudo apt update
```

### 7. Now, install GitLab Community Edition

```
sudo apt install -y gitlab-ce
```

### 8. Configure GitLab

```
sudo gitlab-ctl reconfigure
```

### 9. Access GitLab

Once the configuration is complete, open your web browser and navigate to the server’s IP address or domain name.

If you’re using the IP address, it will look something like `http://<your-server-ip>/`

You should see the GitLab setup page. The default login is:

  - `Username: root`

  - Password: The password was set during installation or can be found in

    ```
    sudo cat /etc/gitlab/initial_root_password
    ```

### 10. Set Up GitLab

Once logged in, you can change the root password and configure GitLab further.


======================END===============================


Setting up GitLab on Windows directly isn't as straightforward as on Linux-based systems because GitLab is primarily designed to run on Linux. 

However, we can still run GitLab on Windows using Windows Subsystem for Linux (WSL) or a virtual machine (VM). 
