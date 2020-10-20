# An alternative version of btmgmt

This is a slightly modified version of btmgmt. The source code is extracted from the official source code of bluez version 5.54. It should compile in Ubuntu 20.04 (bluez 5.53). It works also using Ubuntu 18.04 (bluez 5.48) but there may be some display issues with some characters.

## Compilation

To compile the code, run:
```bash
$ gcc -I./ *.c -lbluetooth -lreadline -o btmgmt-alt
```

Note that you may need to install some packages first, e.g., libreadline-dev. 

## Changes to the official version

The changes made are:
- It now registers for the New Identity Resolving Key event, and prints the IRK. 
Once the IRK is detected, it is saved to a file, whose name is the same as the identity address associated with the IRK, with the following format: 

    ````
    <bluetooth address> (type <address type>) <IRK>
    ````
    For example:

    ````
    18:54:cf:b7:12:ef (type 0) 53ba77b5772f3886f5a841937504bfd5
    ````
- The Device Found event now also prints the EIR data (e.g., service data). This is useful to see the advertisment payload. By default, the EIR data is not shown. To show the EIR data in the scan, use the following command:
    ````
    eir_data on
    ```` 

- Fixed an issue with the 'irks' command. This command can be used to load an existing file containing an IRK. The format of the file is the same as the format of the saved IRK file mentioned above. For example, to load the IRK from the file '18:54:cf:b7:12:ef' run the following in the btmgmt shell: 
    ````
    [mgmt] irks -f 18:54:cf:b7:12:ef
    ````

- Added an option '-r' to the irks command, to reset the IRK list. This removes all IRKs currently registered in the kernel.

