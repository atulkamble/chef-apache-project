---

# chef-workstation-setup-amazon-linux-2023
Basic Chef Workstation Project

This document provides a comprehensive guide for installing and setting up Chef on Amazon Linux 2023. Follow these instructions to ensure proper installation and configuration.

### Launch EC2 and Connect via SSH

1. Launch an Amazon EC2 instance running Amazon Linux 2023.
2. Connect to the instance using SSH.

### Step 1: Update the System

Ensure that all system packages are up-to-date with the latest updates and security patches:

```bash
sudo yum update -y
```

To clone the repository from GitHub, follow these instructions:

### Cloning the Repository

1. **Ensure Git is installed on your system.** If not, install it using the following command:
   
   For Amazon Linux 2023:
   ```bash
   sudo yum install git -y
   ```

2. **Clone the repository using Git.** Open your terminal and run the following command:

   ```bash
   git clone https://github.com/atulkamble/chef-project.git
   ```

3. **Navigate into the cloned repository directory:**

   ```bash
   cd chef-project
   ```


### Step 2: Download and Install Chef Workstation

Chef Workstation is a suite of tools for managing infrastructure and executing Chef recipes.

1. **Download the Chef Workstation package:**

    ```bash
    wget https://packages.chef.io/files/stable/chef-workstation/24.4.1064/el/8/chef-workstation-24.4.1064-1.el8.x86_64.rpm
    ```

2. **Install the downloaded package:**

    ```bash
    sudo rpm -Uvh chef-workstation-24.4.1064-1.el8.x86_64.rpm
    ```

### Step 3: Verify the Installation

Confirm that Chef Workstation is installed correctly by checking the version:

```bash
chef --version
```

### Troubleshooting

If you encounter the error `/opt/chef-workstation/embedded/bin/ruby: error while loading shared libraries: libcrypt.so.1: cannot open shared object file: No such file or directory`, resolve it by installing the necessary compatibility library:

```bash
sudo yum install libxcrypt-compat -y
```

### Step 4: Set Up a Chef Repository

1. **Create a Chef repository:**

    ```bash
    chef generate repo chef-repo
    cd chef-repo
    ```

2. **Create a Cookbook:**

    ```bash
    chef generate cookbook cookbooks/my_cookbook
    cd cookbooks/my_cookbook
    ```

3. **Write a Recipe:**

    Edit the `recipes/default.rb` file in your cookbook:

    ```bash
    nano recipes/default.rb
    ```

    Add the following content:

```ruby
package 'httpd' do
  action :install
end

service 'httpd' do
  action [:enable, :start]
end

file '/var/www/html/index.html' do
  content '<h1>Hello from Chef-provisioned EC2 instance!</h1>'
  mode '0755'
  owner 'apache'
  group 'apache'
end
```

### Step 5: Run Chef Client in Local Mode

Test your cookbook by executing Chef in local mode:

```bash
sudo chef-client --local-mode --runlist recipe[my_cookbook::default]
```
Check Public ip of instance
```
```
