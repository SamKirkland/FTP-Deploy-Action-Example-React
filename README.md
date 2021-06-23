# FTP-Deploy-Action-Example-React
An example of deploying a react project using [FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action).
The following example should work for most frameworks (angular, react, vue, etc)

You can see the results of this deployment by going to [ftp-deploy-action-example-react.samkirkland.com](https://ftp-deploy-action-example-react.samkirkland.com/)

![Build and Publish Front End Framework Website](https://github.com/SamKirkland/FTP-Deploy-Action-Example-React/workflows/Build%20and%20Publish%20Front%20End%20Framework%20Website/badge.svg)

### Secrets
To add a `secret` go to the `Settings` tab in your project then select `Secrets`. Add a new `Secret` for each of the following

| Secret Key Name | Value                                                                |
|-----------------|----------------------------------------------------------------------|
| server          | ftp.samkirkland.com                                                  |
| username        | react-deploy-example@ftp-deploy-action-example-react.samkirkland.com |
| password        | YourPasswordHere                                                     |
| local-dir       | build                                                                |


### YAML config file
The following is the exact contents of `FTP-Deploy-Action-Example-React/.github/workflows/main.yml` file
```
on: push
name: 🚀 Deploy website on push
jobs:
  web-deploy:
    name: 🎉 Deploy
    runs-on: ubuntu-latest
    steps:
    - name: 🚚 Get latest code
      uses: actions/checkout@v2

    - name: Use Node.js 12
      uses: actions/setup-node@v2-beta
      with:
        node-version: '12'
      
    - name: 🔨 Build Project
      run: |
        npm install
        npm run build
    
    - name: List output files
      run: find build/ -print
      
    - name: 📂 Sync files
      uses: SamKirkland/FTP-Deploy-Action@4.1.0
      with:
        server: ftp.samkirkland.com
        username: react-deploy-example@ftp-deploy-action-example-react.samkirkland.com
        password: ${{ secrets.FTP_PASSWORD }}
        local-dir: build/
```
