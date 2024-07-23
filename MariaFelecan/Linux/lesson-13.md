* elevating privilages for a user

- change the user we are using:

    su (abreviation for substitute)

    su -h : all options for arguments for su

    su - username

    to log in back as root: type 'exit'

    -> when we only type 'su', it is assumend that we want to be root, but we will be asked for a password - BUT no password is set for root (privacy concerns) => deadend

- sudo

    -> sudo ps : sudo creates a new session for the ps

    -> sudo -i : we ant to use sudo to switch to a privileged session

- /etc/sudoers file

    -> in this file:
    root ALL=(ALL:ALL) ALL
    this is the configuration line for the user

    %sudo ALL=(ALL) NOPASSWD:ALL
    this is the config for the group
    
    % - character for group

    if we try to use sudo for a user that is not in the sudoers file, we are denied

- editing the sudoers file:

    *version 1: with any editor like vim

    *version2: with visudo

    *to configure what editor to use: update-alternatives --config editor

    










