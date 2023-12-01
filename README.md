## Aim of the Project :-
1.	Create an instance in US-east-1(N.Virginia) region with Linux OS manage the requirement of web servers of your company using AMI.
2.	Replicate the instance in us-west-2(Oregon) region.
3.	Build two EBS Volume and attach them to the instance in us-east-1 (N.Virginia) region.
4.	Delete on volume after detaching it and extend the size of other volume.
5.	Take backup of this EBS volume.

## Solution:

 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/a2a7272a-ce24-4f4d-8c13-66ecd43b8a9c)

### First Step: 
To begin, navigate to the AWS console and select EC2. From there, proceed to launch an instance. Next, add your name and tags, and then select an Amazon Machine Image.  I have chosen Ubuntu. Now it's time to choose the instance type. Since my account is in the free tier, I'll select T2 micro instance. 

![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/2bb28f28-d966-4cf7-93df-1a54a8efe6b6)

### Second step:  
We now need to generate a new login key pair. Afterwards, we need to set up a firewall for our instance. Specifically, we should allow SSH traffic on the network settings, as well as HTTP traffic from the internet. While we may not need HTTP access later on, allowing it initially ensures that people can access the instance via the internet.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/368e1deb-b15f-47d5-93d2-62a504d21d86)

After configuring the storage and selecting 8 GB, which is sufficient, we are now ready to launch an instance.



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/2614bfa5-e16d-4516-b4ed-399d2715004d)

### Third step: 
Now, let's use PuTTY, but before that, we need to convert a key pair using credentials. Finally, we'll input our username to establish a connection to our running instance in PuTTY.
Once connected to the running instance using PuTTY, we can proceed to install Apache 2 by entering the following command:
sudo apt-get install apache2



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/052e6bbc-a2c8-4570-b0d0-f87b00e89f3a)

After installing Apache 2, you can copy your public IP address and paste it into the search option of your web browser. By doing so, you should be able to see the Apache2 default page displayed.Now we have completed the first part, Created a instance in US-east-1(N.Virginia) region with Linux OS.



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/19dfdb63-12ac-44ab-892c-fe4b72d23bea)

### Fourth Step :
Now we’ll install WinSCP. Now  by the help of the winscp we can make a connection to the remote system. WinSCP is a file transfer tool that enables secure copying of files between a local and a remote server using various protocols such as SFTP and SCP. It also allows users to manage remote files with a user-friendly interface. Now to login we need to upload our private key. We can drag the folder from our local machine to ubuntu machine to transfer it. 



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/cf1e9dca-ce31-4562-a200-c8a0c8eb5aa7)

### Fifth Step :
We can clearly see that we have successfully transferred it to our ubuntu machine. Now we have to transfer all these files to /var/ww/html folder, so to achieve that we need to run this command

`sudo apt cp -r /home/ubuntu/picstudio-html/* /var/www/html`



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/b2647d9a-5381-4f8f-b753-50094a28a6cf)

### Sixth Step :
Upon completion of the refresh, the website is now visible, indicating successful hosting on the assigned IP address.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/85cd303b-d45c-4e1a-800a-b52ffa5d8296)

### Seventh Step :
To ensure future ease of replicating this server setup, we'll proceed by packaging it into an Amazon Machine Image (AMI). To initiate this process, navigate to the "Images and Templates" section under the "Actions" tab, and create an image. Specify a name and description for the image to facilitate identification and usage in the future.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/7524c8c1-0864-4588-b7a4-8bfe06a8c766)

### Eight Step :
We can find our newly created AMI in the AMIs tab.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/a97f2b2c-e6ca-44c8-829b-9fa2697c8311)

### Ninth Step :
To create a copy of the AMI for the Oregon Region, switch the region setting from Virginia to Oregon in the top right-hand corner. Locate the previously selected AMI, click on "Actions," and choose the "Copy AMI" option. Specify a name and description for the new AMI. Select "Oregon" as the destination region, and then proceed by clicking on "Copy AMI" to initiate the duplication process.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/4974eccc-a0d3-4284-95cc-c5b946669e7b)

### Tenth Step :
We can check the newly created copy AMI in Oregon region.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/82da531b-4d8e-4a80-bb75-3bbb5de06a1d)

### Eleventh Step :
The next step involves the creation of a new EC2 instance using the previously copied AMI. To initiate this, select the "Launch Instance From AMI" option. We can notice that our own AMI is automatically selected instead of the available ones.



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/6d417191-c6a0-43a6-8230-2b7326821646)

### Twelfth Step :
Upon completion of the process, we can now observe our website successfully deployed on the new public IP. This mirrors the exact replica of the previously deployed website, confirming the successful replication of our desired configuration.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/be1bcfad-5c68-4850-9458-6dc446cde2fb)

### Thirteenth Step :
Now we'll create two EBS volumes and link them to our instance. Navigate to the "Volumes" tab under Elastic Block Store and click on "Create Volume." Specify the size as 2GB and choose the same availability zone as our EC2 instance (in this case, us-east-1b). Optionally, we can add a tag with a name for better identification. 



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/eed5c4b6-4dd2-4bf1-9b70-e657f0ed38b5)

### Fourtheen Step :
Now, we need to connect the recently made 2GB EBS volume to our EC2 instance. Head to "Actions" and click on "Attach Volume" to link the volume to the instance. Confirm the successful attachment, and now we have effectively linked it to our instance. 



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/17856641-a131-4da7-a2d7-dcf4b0d75c14)

### Fifteen Step :
Similarly, we have to create another EBS volume with 4GB size.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/09bb201f-27d2-47ed-a7c4-e6544c36be6b)

### Sixteenth Step :
Now we will Attach the volume to our EC2 instance.



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/6a0353d1-79f4-44fa-81de-a5a755d30779)

### Seventeenth Step :
We can see that both our 2GB and 4GB volume have been successfully attached to our EC2 instance.



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/792b1fdf-fdbd-40a6-9050-1eb445360942)

### Eighteenth Step :
Now we have to delete the 4GB EBS volume and modify the 2GB EBS volume and increase it’s size to 4GB. First, we need to detach the volume, and for that, we'll click on "Detach Volume" in the "Actions" tab. This ensures the volume is safely disconnected from our instance before we proceed with the deletion.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/90369dcf-e538-4eea-89dd-854eed3ef360)
 
### Nineteenth Step :
Now we can delete the 4GB volume.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/a48f5a4e-02c7-4935-9b70-e61b3e0730ec)

### Twentieth Step :
Now we have to modify the 2GB EBS volume. We will click on Modify Volume under Actions tab and change the size to 4GB.



 ![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/2491baeb-2eee-4206-a081-f06036b5c7f4)

### Twenty-first Step :
Observing our instance, we can confirm that the 2GB volume has been successfully modified, now reflecting a size of 4GB. Simultaneously, the 4GB volume has been detached, completing the necessary updates to our storage configuration.



![image](https://github.com/satyamaatmdeep10/Secure-Web-Servers-On-Linux/assets/137147966/cd2f04d4-e5e0-4137-b35b-4ef8722827fc)

### Twenty-Second Step :
Now we have to create a snapshot of the EBS volume. To ensure a backup of our EBS volume, proceed by selecting the "Snapshot" option under the Elastic Block Store tab. Click on "Create Snapshot," choose the relevant EBS volume from the dropdown menu, and provide a meaningful description. With these steps, our backup is successfully created, offering an additional layer of data protection.
