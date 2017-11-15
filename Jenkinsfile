node ('int-jenkinsnode') {
    
 stage ('SCM_Checkout') {
    checkout([$class: 'GitSCM',
        branches: [[name: '*/master']],
        doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [],
        userRemoteConfigs: [[url: 'https://github.com/ganeshhp/PetClinicProject-Int.git']]])
 }
 stage ('Build_Test and Package') {
    sh 'mvn clean verify package'
    junit 'target/surefire-reports/TEST*.xml'
 }
 
 stage ('Archive and Notify') {
    publishHTML(target: [allowMissing: true,
                 alwaysLinkToLastBuild: false,
                 keepAll: true,
                 reportDir: 'target/site/jacoco',
                 reportFiles: 'index.html',
                 reportName: 'HTML Report',
                 reportTitles: 'Code Coverage-Report'])
    archiveArtifacts 'target/*.war'
 }
}
