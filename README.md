# Port-Scanner
This tool scans ports on a specified host using Python
In this version of the script, the `scan_ports()` function uses the `threading` module to create a separate thread for each port to be scanned. 
The `scan_port()` function is the target of each thread, and it's responsible for checking if the specified port is open. 
This allows multiple ports to be checked simultaneously, which should result in faster overall scanning times.

The `join()` method is used to wait for all the threads to finish before the script exits. 
The open ports are not collected in a list, the script prints the open ports as it finds them, you can remove the print statement if you don't want the open ports to be displayed.


This version of the script includes several improvements to handle more specific exceptions and validate user input:

It uses regular expression to check if the input for host is a valid hostname or IP address.
It handles `socket.timeout` exception specifically in the `scan_port` function, so that it can print a more informative message when timeout occurs while connecting to a port.
It also uses `socket.inet_aton` method to check if the input host
