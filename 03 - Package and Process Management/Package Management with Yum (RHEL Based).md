# Package Management with Yum (RHEL Based)

### 1. Introduction to Yum

Yum (Yellowdog Updater Modified) is the primary package management tool for Red Hat Enterprise Linux (RHEL) and its derivatives like CentOS and Fedora. It allows you to install, update, and remove software packages while automatically handling dependencies.

### 2. Basic Yum Commands

- Searching for packages:
`yum search keyword`

- Getting information about a package:
`yum info package_name`

- Installing a package:
`sudo yum install package_name`

-  Removing a package:
`sudo yum remove package_name`

-  Updating all packages:
`sudo yum update`

- Updating a specific package:
`sudo yum update package_name`

### 3. Working with Repositories

Yum uses repositories to fetch package information and the packages themselves. 

- Listing enabled repositories:
`yum repolist`

- Listing all repositories (including disabled):
`yum repolist all`

- Adding a new repository:
Create a .repo file in /etc/yum.repos.d/ with the following structure:

```
[repository_id]
name=Repository Name
baseurl=http://repository.url
enabled=1
gpgcheck=1
gpgkey=http://repository.url/RPM-GPG-KEY
```

- Enabling/disabling a repository: 
 - `sudo yum-config-manager --enable repository_id`
 - `sudo yum-config-manager --disable repository_id`

### 4. Managing Package Groups

Yum can install predefined groups of packages.

- Listing available groups:
`yum group list`

- Getting info about a group:
`yum group info "group_name"`

- Installing a group:
`sudo yum group install "group_name"`

- Removing a group:
`sudo yum group remove "group_name"`

### 5. Yum Cache Management

Yum maintains a cache to speed up operations.

- Cleaning all cached packages and metadata:
`sudo yum clean all`

- Cleaning only cached packages:
`sudo yum clean packages`

- Cleaning only cached metadata:
`sudo yum clean metadata`

### 6. Advanced Yum Features

- Downloading a package without installing:
`yumdownloader package_name`

- Installing a local RPM package with Yum (to resolve dependencies):
`sudo yum localinstall package_name.rpm`

- Checking for available updates:
`yum check-update`

- Listing installed packages:
`yum list installed`

- Listing available packages:
`yum list available`

### 7. Yum History

Yum keeps a history of transactions, allowing you to undo or redo actions.

- Viewing Yum history:
`yum history list`

- Undoing a transaction:
`sudo yum history undo transaction_id`

- Redoing a transaction:
`sudo yum history redo transaction_id`

### 8. Yum Configuration

The main Yum configuration file is `/etc/yum.conf` Here are some important settings:

- cachedir: Directory where Yum stores its cache files
- keepcache: Whether to keep the cache after successful operations
- debuglevel: Level of debugging output
- gpgcheck: Whether to perform GPG signature checking on packages
- plugins: Whether to enable Yum plugins

### 9. Yum Plugins

Yum's functionality can be extended with plugins. Some useful plugins include:

- yum-plugin-fastestmirror: Finds the fastest mirror for downloads
- yum-plugin-security: Allows security-related operations
- yum-plugin-versionlock: Locks specified packages to a particular version

To install a plugin:
`sudo yum install plugin_name`

### 10. Troubleshooting

If you encounter issues with Yum, try these steps:

- Clear the Yum cache:
`sudo yum clean all`

- Rebuild the Yum cache:
`sudo yum makecache`

- Check for conflicting transactions:
`sudo yum-complete-transaction --cleanup-only`

- Verify the package database:
`sudo yum check`
