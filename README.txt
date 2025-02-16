S3 Bucket Installation Setup:
Source: https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html

URL: http://swe645-task-1.s3-website-us-east-1.amazonaws.com/

1. Create an S3 bucket (Enter bucket name and select region)
2. Enable static website hosting
3. Edit Block Public Access settings
4. Add a bucket policy that makes your bucket content publicly available
5. Configure an index document (Upload following content)
	a. index.html
	b. Profile_Pic.jpg
	c. homePageStyles.css
	d. George-Mason-University-New.png
6. Configure an error document (Upload following content)
	a. error.html
	b. error.css
7. Test website endpoint:
	Buckets -> Properties -> Under 'Static Website Hosting', select 'Bucket website endpoint'

EC2 Instance Set up:
Source: https://www.youtube.com/watch?v=0Gz-PUnEUF0
https://www.youtube.com/watch?v=SwXk5K9I3rI&list=LL&index=1

URL: http://ec2-54-165-122-225.compute-1.amazonaws.com/student-survey-form.html

1. Search for EC2 instance on AWS console and launch the service
2. At the EC2 instance dashboard, select Instances under the Instances menu
3. Select 'Launch Instance'
4. Enter name/tag of the EC2 instance
5. Select 'Ubuntu Server 24.04 LTS (HVM), SSD Volume Type' AMI
6. Select t2.micro for 'Instance Type'
7. Under 'Key pair', create a new key pair 
	a. Enter 'Key pair name' 
	b. RSA Key Pair type 
	c. .ppk (Private key file format)
8. Configure security group 
	a. Allow SSH (Port 22)
	b. Allow HTTP (Port 80)
9. Launch instance
10. Select the newly created instance and 'Connect'
11. Use default 'Connection Type' and 'Public IPv4 address'
12. Under 'Username' enter 'root'

Putty (SSH) Configuration:

1. Copy IP address of the instance (Public IPv4 address)
2. Enter the default user (ubuntu) and paste the IP address in the 'Host Name' field'
	Full Host Name: ubuntu@44.203.162.85
3. Enter '22' for Port Number
4. Add a name for the 'new stored session'
5. Apply SSH Private key
	a. Under the Category window navigate to 'SSH Auth Credentials'
		Connection -> SSH -> Auth -> Credentials
	b. Select browse private key file
	c. In the File Explorer window, search and select private key file
6. Navigate back to 'Session' window and save the current session.
7. Open connection

After environment is all set up, run the following commands to install Apache web server on AWS Console CMD as 'root' user:

sudo apt update
sudo apt install apache2 -y

After installation, start and enable Apache:

sudo systemctl start apache2
sudo systemctl enable apache2

Grant permission to ubuntu User:

sudo chown -R ubuntu:ubuntu /var/www/html/
sudo chmod -R 775 /var/www/html/

FTP Client:

Enter Key Pair:
  1. Download FileZilla
  2. Edit -> Settings -> SFTP Page
  3. Select 'Add Key File'
  4. Select .ppk file
  5. Click 'Ok' on the bottom left window

Site Manager
  1. Open FileZilla -> Site Manager
  2. Click 'New Site'
  3. Rename Site (optional)
  4. For Protocol, Select 'SFTP - SSH File Transfer Protocol'
  5. Host: 'ec2-ip-address'
  6. Port: '22'
  7. User: 'ubuntu'
  8. Click Ok (save password)
  9. Connect to newly created site

Upload Files:
  1. Navigate to /var/www/html/ and upload files (survey form html/css file/logo)
	a. student-survey-form.html
	b. studentSurveyFormStyles.css
	c. George-Mason-University-New.png

Test Web Server:
  1. http://your-ec2-ip/student-survey-form.html




