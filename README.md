# Hosting a Static Website on AWS S3 with CloudFront, Route 53, and ACM

## Overview
This guide explains how to host a static website using **Amazon S3**, **CloudFront**, **Route 53**, and **ACM (AWS Certificate Manager)** for a secure **HTTPS** connection with a custom domain.

---

## **Architecture Flow**

1. **Amazon S3** → Stores your website's static files (HTML, CSS, JS, etc.).
2. **CloudFront** → Fetches and caches files from S3 for faster performance.
3. **ACM (AWS Certificate Manager)** → Provides an **SSL certificate** to enable HTTPS.
4. **Route 53** → Maps your **custom domain** to CloudFront.

```
User 🔗 → Route 53 (DNS) 🔗 → CloudFront (CDN) 🔗 → S3 (Website Files)  
                    🔗 → ACM (SSL for HTTPS)  
```

---

## **Step-by-Step Setup**

### **1️⃣ Create an S3 Bucket for Hosting**
1. Go to the AWS **S3** console.
2. Click **Create Bucket** and enter your domain name (e.g., `yourdomain.com`).
3. **Disable Block Public Access**.
4. Enable **Static Website Hosting** and note the **endpoint URL**.

![image](https://github.com/user-attachments/assets/b31b11ac-9e4b-4506-8f57-4ec86f8f5b10)
![image](https://github.com/user-attachments/assets/c640efa6-f26b-4f5a-a1cb-438fc08c1ad4)


---

### **2️⃣ Request an SSL Certificate (ACM)**
1. Open **AWS Certificate Manager (ACM)**.
2. Click **Request a certificate** → Select **Public Certificate**.
3. Enter your domain (`dev53p.site` and `www.dev53p.site`).
4. Choose **DNS Validation** (Easier than email validation).
5. Add the provided **CNAME record** in Route 53 and validate.

![image](https://github.com/user-attachments/assets/703793aa-4ac8-4919-9cf0-52851e41508d)

---

### **3️⃣ Create a CloudFront Distribution**
1. Open **CloudFront** in AWS.
2. Click **Create Distribution**.
3. Under **Origin**, choose **S3 Bucket Endpoint**.
4. In **Default Cache Behavior**, select:
   - **Viewer Protocol Policy** → Redirect HTTP to HTTPS.
5. Under **Custom SSL Certificate**, choose the **ACM certificate**.
6. Deploy the CloudFront distribution and note the **CloudFront domain** (`dev53p.site`).

![image](https://github.com/user-attachments/assets/ae684fa0-d858-410c-8b50-46c2c4c5c0ee)
![image](https://github.com/user-attachments/assets/78de0c53-1a1c-4512-b5e1-9ea718f27a9c)


---

### **4️⃣ Configure Route 53 (Domain Mapping)**
1. Open **Route 53** → Click your domain (`dev53p.site`).
2. Create an **A Record (Alias)**.
3. Select **Alias Target** → Choose your **CloudFront Distribution**.
4. Save the record.

![image](https://github.com/user-attachments/assets/e67c4e48-d34b-42bb-8df8-4f4c1f7c3676)

---

## **Test Your Website**
- Open **https://dev53p.site**.
- It should load from **CloudFront** with HTTPS enabled.

✅ **Congratulations!** You have successfully hosted your static website on **AWS S3 with CloudFront, Route 53, and ACM**! 🎉

![image](https://github.com/user-attachments/assets/c92139c6-6434-4f40-a17d-7cfb6904790e)
![image](https://github.com/user-attachments/assets/a77a48fb-6fc4-4314-bde4-86f3ba386dc9)


---

## **Troubleshooting**
- If HTTPS is not working, verify that **CloudFront is using the correct ACM certificate**.
- If the domain doesn’t resolve, ensure **Route 53 has the correct alias record**.
- If CloudFront is not serving updated content, try **Invalidating the Cache** in CloudFront.

Benefits of This Setup

Scalability – S3 automatically scales to handle any traffic volume.

High Availability – AWS ensures 99.99% uptime.

Security – ACM provides free SSL certificates, and CloudFront improves security.

Performance – CloudFront caches content globally for faster access.

Cost Efficiency – Only pay for storage and data transfer.

Custom Domain – Easily set up with Route 53 for professional branding.

DDoS Protection – CloudFront and AWS Shield protect against attacks.

Conclusion

Using AWS S3 with CloudFront, Route 53, and ACM provides a reliable, secure, and scalable way to host a static website. This approach removes the need for traditional web servers, reducing complexity and cost while ensuring global performance.

Now your website is live and secured with HTTPS! 🎉

