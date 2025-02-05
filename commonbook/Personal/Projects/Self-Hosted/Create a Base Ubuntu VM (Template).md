1. **New VM in Hyper-V**

	• Name: Ubuntu-Template

	• Generation 2 if supported

	• Assign CPU, RAM (≥2GB)

	• Attach Ubuntu Server ISO

2. **Install Ubuntu Server**

	• Create an admin user

	• sudo apt update && sudo apt upgrade -y

3. **Enable SSH**

	• sudo apt install -y openssh-server
	
	• sudo systemctl enable ssh && sudo systemctl start ssh

4. **Export or Create Checkpoint**

	• This becomes your “golden image” or template.