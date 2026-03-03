🔍 Process Breakdown
1. Opening the File
I used the with open() statement with the "r" (read) mode. This is a security best practice because it ensures the file resource is properly released even if an error occurs during execution.

2. Converting String to List
The .read() method imports the file contents as a single string. To remove specific IPs, I used .split() to convert that string into a list, making each IP an individual element.

3. Iterating and Removing
I implemented a for loop to check each IP in the remove_list. By including an if statement (if element in ip_addresses:), I ensured the script only attempts to remove IPs that are actually present, preventing "Value Errors" during the cleanup.

4. Updating the File
Finally, I converted the list back into a string using .join() and used the "w" (write) mode to overwrite the old file with the new, secured list.

🚀 Security Value
This script demonstrates the Principle of Least Privilege by ensuring that only authorized users maintain access to critical infrastructure. Automation like this is essential for Incident Response when a set of IP addresses must be blocked immediately following a detected threat.

# Function to update the allow list by removing unauthorized IPs
def update_allow_list(import_file, remove_list):
    # 1. Open the file and read the current allowed IPs
    with open(import_file, "r") as file:
        ip_addresses = file.read()

    # 2. Convert the string of IPs into a list for easy manipulation
    ip_addresses = ip_addresses.split()

    # 3. Iterate through the remove_list to find and remove unauthorized IPs
    for element in remove_list:
        if element in ip_addresses:
            ip_addresses.remove(element)

    # 4. Convert the list back into a string format to save to the file
    ip_addresses = " ".join(ip_addresses)

    # 5. Overwrite the original file with the updated security list
    with open(import_file, "w") as file:
        file.write(ip_addresses)
    
    print("Security Update Complete: Unauthorized IPs have been revoked.")

# Example usage:
# List of IPs that have lost their security clearance
unauthorized_ips = ["192.168.1.105", "10.0.0.45", "172.16.5.12"]

# Running the update on the server's allow list
update_allow_list("allow_list.txt", unauthorized_ips)
