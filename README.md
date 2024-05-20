# example-apigee-proxy

## Purpose
- configure an initial call to the outbound target endpoint (https) to an authentication endpoint which generates a key (username & password provided in the JSON body of the request),
- the token from previous step is then sent to the actual target endpoint to retrieve the actual business information

To achieve this in Apigee Edge, you need to configure a multi-step API proxy that first calls an authentication endpoint to retrieve a token and then uses that token to call the actual target endpoint. Here are the steps and examples of code required to set this up:

### **Step 1: Create the API Proxy**
Login to **Apigee Edge** and go to the API Proxies section.
Click on + API Proxy to create a new proxy.
Select **Reverse** Proxy, provide the necessary details (e.g., name, base path), and click Next.
Configure the **Target Endpoint** to point to the actual business endpoint.
Click Next, Next, and Build and Deploy.

### **Step 2: Configure the Authentication Call**
Open your newly created proxy and navigate to the Develop tab.
Create a new **PreFlow** in the **ProxyEndpoint** section.
Add a **ServiceCallout** policy to call the authentication endpoint.
Extract the token from the response using an **ExtractVariables** policy.

### **Step 3: Use the Token in the Target Request**
Add an **AssignMessage** policy to set the Authorization header for the target request.
Attach the policies in the appropriate flow to ensure they execute in the correct order. Typically, you would attach them to the **PreFlow** of the **ProxyEndpoint**.
Make sure your TargetEndpoint is configured to point to the actual business endpoint.

## Summary
Create a new API proxy.
Configure a ServiceCallout policy to call the authentication endpoint.
Use an ExtractVariables policy to extract the token from the response.
Set the token in the Authorization header using an AssignMessage policy.
Ensure the policies are executed in the correct order in the PreFlow of the ProxyEndpoint.
This setup ensures that your API proxy first authenticates to get a token and then uses that token to make the actual business call.
