# FTP-Deploy-Action-Example-React
An example of deploying a react project using [FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action).
The following example should work for most frameworks (angular, react, vue, etc)

You can see the results of this deployment by going to [ftp-deploy-action-example-react.samkirkland.com](https://ftp-deploy-action-example-react.samkirkland.com/)

![Build and Publish Front End Framework Website](https://github.com/SamKirkland/FTP-Deploy-Action-Example-React/workflows/Build%20and%20Publish%20Front%20End%20Framework%20Website/badge.svg)

### Secrets
To add a `secret` go to the `Settings` tab in your project then select `Secrets`. Add a new `Secret` for each of the following

| Secret Key Name | Value                                                                |
|-----------------|----------------------------------------------------------------------|
| ftp-username    | react-deploy-example@ftp-deploy-action-example-react.samkirkland.com |
| ftp-password    | YourPasswordHere                                                     |
| ftp-server      | ftp.samkirkland.com:21                                               |
| local-dir       | build                                                                |


### YAML config file
The following is the exact contents of `FTP-Deploy-Action-Example-React/.github/workflows/main.yml` file
```
on: push
name: Build and Publish Front End Framework Website
jobs:
  FTP-Deploy-Action:
    name: FTP-Deploy-Action
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
      with:
        fetch-depth: 2

    - name: Use Node.js 12.x
      uses: actions/setup-node@v1
      with:
        node-version: '12.x'
        
    - name: Build Project
      run: |
        npm install
        npm run build --if-present
        
    - name: List output files
      run: find build/ -print
      
    - name: FTP-Deploy-Action
      uses: SamKirkland/FTP-Deploy-Action@3.1.1
      with:
        ftp-server: ftp://ftp.samkirkland.com/
        ftp-username: ${{ secrets.FTP_USERNAME }}
        ftp-password: ${{ secrets.FTP_PASSWORD }}
        local-dir: build
```
