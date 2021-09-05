Reference: 

Node Red HTTPS: https://www.youtube.com/watch?v=z9a_ztJqaII&t=681s

Azure Linux VM and Putty SSH: https://www.youtube.com/watch?v=DzeZGUHWTk0

Running on Microsoft Azure: https://nodered.org/docs/getting-started/azure

To build your own SharePoint, you need a Microsoft Developer account: https://developer.microsoft.com/en-us/microsoft-365/dev-program


Step 1. Go to your Node-Red location
cd / home / yuxiang (your username) / .node-red

Step 2. Generate 1024 bytes certificate
openssl genrsa -out privkey.pem 1024


Step 3. use private key to create Certificate Signing Request
 openssl req -new -key privkey.pem -out private-csr.pem 

Step 4. use Certificate Signing Request to generate Certificate
openssl x509 -req -days 365 -in private-csr.pem -signkey privkey.pem -out cert.pem

Step  5. modify the settings.js file
nano / home / yuxiang (your username) / .node-red

Step 6. add this line before any code:          var fs = require("fs");

Step 7. uncomment the following:   
https: {
        key: require("fs").readFileSync('/home/yuxiang/.node-red/privkey.pem'),
        cert: require("fs").readFileSync('/home/yuxiang/.node-red/cert.pem')
},

Step 8. Control S to save and Control X to exit

Step 9. re-Launch your node-red
node-red
you should see: Server now running at https://127.0.0.1:1880/ in the command prompt



