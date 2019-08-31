# FTP-Deploy-Action-Example-React
An example of deploying a react project using FTP-Deploy-Action.
The following example should work for most frameworks (angular, react, vue, etc)

### Secrets
To add a `secret` go to the `Settings` tab in your project then select `Secrets`. Add a new `Secret` for each of the following

| Secret Key Name | Value |
|-----------------|-------------|
| FTP_USERNAME    | react-deploy-example@ftp-deploy-action-example-react.samkirkland.com |
| FTP_PASSWORD    | YourPasswordHere |
| FTP_SERVER      | ftp.samkirkland.com:21 |
| LOCAL_DIR       | build |


### YAML config file
The following is the exact contents of `FTP-Deploy-Action-Example-React/.github/workflows/main.yml` file
```
name: Build and Publish React Website

on: [push]

jobs:
  build:
  
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@master
    
    - name: Use Node.js 12.x
      uses: actions/setup-node@v1
      with:
        node-version: '12.x'
        
    - name: Build Project
      run: |
        npm install
        npm run build --if-present
        
    - name: List output files
      run: ls
      
    - name: FTP-Deploy
      uses: SamKirkland/FTP-Deploy-Action@master
      env: 
       FTP_SERVER :  ${{ secrets.FTP_SERVER }}
       FTP_PASSWORD :  ${{ secrets.FTP_PASSWORD }}
       FTP_USERNAME :  ${{ secrets.FTP_USERNAME }}
       LOCAL_DIR : ${{ secrets.LOCAL_DIR }}

```

