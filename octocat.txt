import requests

def update_bios(bios_file_path, bmc_url, username, password):
    # Read the BIOS binary file
    with open(bios_file_path, 'rb') as bios_file:
        bios_content = bios_file.read()

    # Set up the headers
    headers = {
        'Content-Type': 'application/octet-stream',
    }

    # Set up authentication
    auth = (username, password)

    # Make the POST request to update BIOS
    update_url = f"{bmc_url}/Actions/UpdateService.SimpleUpdate"
    response = requests.post(update_url, data=bios_content, headers=headers, auth=auth)

    # Check if the request was successful
    if response.status_code == 200:
        print("BIOS updated successfully!")
    else:
        print("Failed to update BIOS. Status code:", response.status_code)

# Example usage
bios_file_path = 'bios_update_file.bin'
bmc_url = 'https://example-bmc.com/redfish/v1/UpdateService'
username = 'your_username'
password = 'your_password'

update_bios(bios_file_path, bmc_url, username, password)
