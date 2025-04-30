<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Website Delivery with CloudFront

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-cloudfront)

**Author:** Vijay Pratap Singh Hada  
**Email:** vijaypratapsinghhada9@gmail.com

---

## Website Delivery with CloudFront

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-networks-cloudfront_1dddddwe)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use CloudFront(CDN) to deliver website content fast globally. I'm doing this project to learn about CDNs(content delivery network),to understand how things work behind the scenes in presentation tier of a 3-Tier Architecture. 

### Tools and concepts

Services I used were Amazon S3 for storing my website files and Amazon CloudFront as a content delivery network (CDN) to distribute that content efficiently. Key concepts I learned include the importance of a CDN in speeding up access to a website by caching files closer to users around the world. Additionally, I gained insight into setting permissions and policies for S3 buckets to ensure content security.  Understanding static website hosting and how to use developer tools to analyze website performance were also crucial concepts that contributed to my overall knowledge in web hosting and content delivery.

### Project reflection

This project took me approximately 2 hours and 30 minutes to complete. It was most rewarding to see my website functioning properly with fast load times once I implemented CloudFront. Being able to compare the performance of CloudFront and S3 hosting helped me understand the advantages of using a CDN, and successfully navigating the setup process gave me confidence in my web hosting skills

I did this project today to enhance my skills in web hosting and content delivery using AWS. It met my goals by providing hands-on experience with both Amazon S3 and CloudFront, allowing me to understand their functionalities and performance differences.

---

## Set Up S3 and Website Files

I started the project by creating an S3 bucket to store the files for my website. I can't use CloudFront for this task because CloudFront doesn’t store files itself; it only delivers content that is stored elsewhere, like in an S3 bucket, to users around the world. By using S3, I ensure a reliable place to keep my website files, which can then be accessed quickly through CloudFront.

The three files that make up my website are index.html, which is the main file that structures the entire webpage. It organizes the content and links to style.css, which defines how the website looks, such as the colors and fonts. Then there’s script.js, which adds functionality by providing instructions for interactions on the website, allowing things to move or change when users interact with different elements. 

I validated that my website files work by opening the index.html file in my web browser. When I see the user interface of the website, it confirms that my files are uploaded successfully to the S3 (Simple Storage Service) bucket without any issues. This means everything is set up correctly and ready to be used, showing that the files are working as intended.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-networks-cloudfront_qgo7wcd3)

---

## Exploring Amazon CloudFront

Amazon CloudFront is a content delivery network (CDN), which means it helps speed up how your website content is distributed all over the world. Businesses and developers use CloudFront because it stores copies of files in temporary locations, making them easier to access quickly. This caching system allows users to receive content with low latency, ensuring that our website loads fast and performs well. With CloudFront, visitors around the globe get a better experience as they access your website content quickly and efficiently.




To use Amazon CloudFront, you set up distributions, which are sets of instructions that tell CloudFront how to deliver your content effectively. I set up a distribution for my S3 bucket, which stores my website's files. The origin is where my content is stored, and in this case, it's my S3 bucket named "nextwork-three-tier." By configuring this distribution, I ensure that CloudFront knows how to access and serve my website's files to users quickly and efficiently from around the world.

My CloudFront distribution's default root object is set to index.html. This means that whenever someone visits the main URL of my website, CloudFront will automatically serve the index.html file. By choosing this file as the default root object, I ensure that visitors see the correct webpage immediately when they access my site. This setup helps create a smooth and user-friendly experience, making it easier for users to find the information they need right from the start.





![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-networks-cloudfront_qgo7wcdt)

---

## Handling Access Issues

When I tried visiting my distributed website, I ran into an access denied error because CloudFront does not have permission to access my S3 bucket. By default, S3 buckets are set to private, which means they don’t allow access to anyone unless specific permissions are granted. This is expected behavior, and it reminds me that I need to configure the settings to give CloudFront the necessary access to the files stored in my bucket before my website can be viewed properly.

My distribution's origin access settings were set to public by default. This caused the access denied error because even though public access means anyone can directly access content from the origin, it doesn't automatically change the permissions for the objects in the S3 bucket. By default, S3 bucket objects remain private, so even with public origin access, my website couldn't be viewed until I updated the permissions of those objects to allow everyone to access them. 



To resolve the error, I set up origin access control (OAC). OAC is a special user for CloudFront that allows access to my S3 bucket and its objects without making them publicly accessible. This means my content remains secure from unwanted access while still being accessible through CloudFront. OAC also gives me more control over how CloudFront accesses my files, allowing me to add additional security measures to ensure only authorized users can view my content. This setup helps protect my data while delivering it efficiently.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-networks-cloudfront_egrhntyu)

---

## Updating S3 Permissions

Once I set up my origin access control (OAC), I still needed to update my bucket policy because CloudFront requires specific permissions to access the files inside my S3 bucket. The OAC ensures that only CloudFront can retrieve these files, but it does not automatically grant permission to access the bucket's contents. Therefore, I must update the S3 bucket's policy to explicitly allow the OAC permission to access the files stored within the bucket.



Creating an origin access control (OAC) automatically gives me a policy I could copy, which grants CloudFront permission to access the files in my S3 bucket. This policy ensures that only requests coming from CloudFront are allowed to retrieve content from the bucket, thus keeping my files secure from direct public access. By pasting this policy into the bucket’s settings, I make sure that CloudFront can safely and effectively deliver my website's content while preventing unauthorized users from accessing it directly.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-networks-cloudfront_eg98ntyu)

---

## S3 vs CloudFront for Hosting

For my project extension, I'm comparing using CloudFront versus S3 to serve my website. I initially had an error with static website hosting because, even after enabling the static website option, my S3 bucket permissions were not set correctly. By default, S3 buckets are private, so I needed to adjust the permissions to allow public access to the files. Without the right permissions, anyone trying to access my website will encounter the 403 Forbidden error, which means they don't have permission to view the content. 

I tried resolving this by unchecking the "Block all public access" setting in my S3 bucket, thinking it would allow visitors to access the website. However, I still ran into an error because simply changing this setting does not automatically grant permission to view the files stored in the bucket. It only stops blocking public access attempts. I still need to create a bucket policy that explicitly allows public read access to the objects in my bucket. This policy is essential to inform AWS that anyone on the internet should be able to read the files, ensuring my static website is accessible to all users.

I could finally see my S3 hosted website when I updated the bucket policy to allow public read access. This worked because I added a specific statement that granted permission for anyone to get objects from my S3 bucket. By replacing the placeholder with my actual bucket name and ensuring the policy was correctly formatted, I told AWS that all users should be able to view the files in my bucket. After saving the changes and refreshing the bucket's website endpoint URL, I was able to access my site without any errors. This change made my content readily available to visitors online.

Compared to the permission settings for my CloudFront distribution, using S3 meant that I had to make my files publicly accessible to serve a static website directly. In CloudFront, I can keep my S3 bucket private and use origin access control to manage who can access my content securely. I preferred using CloudFront because it allows me to maintain better security while delivering my content efficiently. With CloudFront, I have more control over access permissions, ensuring that only authorized users can retrieve files while still providing fast delivery to my website visitors. 

---

## S3 vs CloudFront Load Times

Load time means how quickly content on a website appears for users. The load times for the CloudFront site were faster than the S3 site because CloudFront uses a content delivery network (CDN) that caches files at locations closer to users around the world. This allows data to travel shorter distances, leading to quicker access. In contrast, the S3 static website hosting serves files directly from a single region, meaning users farther away from that region experience longer load times. By leveraging CloudFront, I can ensure that my website loads faster for visitors, providing them with a better browsing experience overall.

A business would prefer CloudFront when it needs to deliver content quickly and efficiently to users across the globe, as it uses a content delivery network (CDN) to cache files closer to users, improving load times. This is especially important for sites with heavy traffic or users in different regions. S3 static website hosting might be sufficient when the website has a smaller audience, mainly local users, or when content doesn't require fast delivery, and security concerns are minimal. For basic websites without complex performance needs, S3 can effectively serve static content without the added complexity of using CloudFront.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-networks-cloudfront_12verpuh)

---

---
