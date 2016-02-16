## 1. Get the awesome_customers cookbook

You can skip this step if you already have the `awesome_customers` cookbook on your workstation.

### Option 1: Download the zip file from GitHub

Download the `awesome_customers` project as a zip file from GitHub and extract it to the <code class="file-path">~/manage-a-web-app-ubuntu</code> directory on your workstation.

<a class='accent-button radius' href='https://github.com/learn-chef/manage-a-web-app-ubuntu' target='_blank'>Download the awesome_customers project&nbsp;&nbsp;<i class='fa fa-external-link'></i></a>

![Download a zip file from GitHub](tutorials/github-zip.png)

### Option 2: Clone the GitHub repo

If you're a Git user, you can clone the GitHub repo.

```bash
$ cd ~
$ git clone https://github.com/learn-chef/manage-a-web-app-ubuntu.git
```

[COMMENT] You can extract the zip file or clone the Git repo to a different directory if you'd like. Just remember to adjust the paths you see in this tutorial as needed.

### Encrypt your data bags

You'll also need to generate a new secret key and use it to encrypt the local version of your data bags.

First, run the command that matches your workstation setup to generate your secret key file.

### From a Linux or Mac OS workstation

```bash
# ~/chef-repo
$ openssl rand -base64 512 | tr -d '\r\n' > /tmp/encrypted_data_bag_secret
```

### From a Windows workstation

```ps
# ~\chef-repo
$ $key = New-Object byte[](512)
$ $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($key)
$ [Convert]::ToBase64String($key) | Out-File "C:\temp\encrypted_data_bag_secret" -encoding "UTF8"
$ [array]::Clear($key, 0, $key.Length)
```

Now, modify <code class="file-path">~/manage-a-web-app-ubuntu/chef-repo/data\_bags/passwords/sql\_server\_root\_password.json</code> by adding the SQL root password in plain text.

```ruby
# ~/manage-a-web-app-ubuntu/chef-repo/data_bags/passwords/sql_server_root_password.json
{
  "id": "sql_server_root_password",
  "password": "learnchef_mysql"
}
```

Now modify <code class="file-path">~/manage-a-web-app-ubuntu/chef-repo/data\_bags/passwords/db\_admin\_password.json</code> by adding the database password.

```ruby
# ~/manage-a-web-app-ubuntu/chef-repo/data_bags/passwords/db_admin_password.json
{
  "id": "db_admin_password",
  "password": "database_password"
}
```

Finally, encrypt your MySQL and database passwords locally.

### From a Linux or Mac OS workstation

```bash
# ~/manage-a-web-app-ubuntu/chef-repo
$ knife data bag from file passwords sql_server_root_password.json --secret-file /tmp/encrypted_data_bag_secret --local-mode
Updated data_bag_item[passwords::sql_server_root_password]
$ knife data bag from file passwords db_admin_password.json --secret-file /tmp/encrypted_data_bag_secret --local-mode
Updated data_bag_item[passwords::db_admin_password]
```

### From a Windows workstation

```ps
# ~\manage-a-web-app-ubuntu\chef-repo
$ knife data bag from file passwords sql_server_root_password.json --secret-file C:\temp\encrypted_data_bag_secret --local-mode
Updated data_bag_item[passwords::sql_server_root_password]
$ knife data bag from file passwords db_admin_password.json --secret-file C:\temp\encrypted_data_bag_secret --local-mode
Updated data_bag_item[passwords::db_admin_password]
```