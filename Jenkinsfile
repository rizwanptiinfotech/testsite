//Address of source code
String githubUrl = "https://github.com/rizwanptiinfotech/testsite.git"

//The name of the project in the source code
String projectName = "testsite"

//The directory where the source code will be published
String publishedPath = "testsite\\publish"

//The name of your site defined in IIS on the target machine
String iisApplicationName = "testsite"

//Your site's directory defined in IIS on the target machine
String iisApplicationPath = "C:\\inetpub\\wwwroot\\testsite"

//IP of the target machine
String targetServerIP = "10.0.21.41"

node () {
    stage('Checkout') {
        checkout([
            $class: 'GitSCM', 
            branches: [[name: 'master']], 
            doGenerateSubmoduleConfigurations: false, 
            extensions: [], 
            submoduleCfg: [], 
            userRemoteConfigs: [[url: """ "${githubUrl}" """]]])
    }
    stage('Build') {
        echo 'Building..'
        // bat """
        // cd ${projectName}
        // dotnet build -c Release /p:Version=${BUILD_NUMBER}
        // dotnet publish -c Release --no-build
        // """
    }
    stage('Deploy'){
        withCredentials([usernamePassword(credentialsId: '0f337fcc-397b-4c0c-93ee-ac820db81748', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) { bat """ "C:\\Program Files (x86)\\IIS\\Microsoft Web Deploy V3\\msdeploy.exe" -verb:sync -source:iisApp="${WORKSPACE}" -enableRule:AppOffline -dest:iisApp="${iisApplicationName}",ComputerName="https://${targetServerIP}:8172/msdeploy.axd",UserName="$USERNAME",Password="$PASSWORD",AuthType="Basic" -allowUntrusted"""}
    }
}
