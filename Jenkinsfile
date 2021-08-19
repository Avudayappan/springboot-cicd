node {
  def image
   //1//  stage ('checkout') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/Avudayappan/springboot-cicd.git']]])      
        }
   
 //2//   stage ('Build') {
         def mvnHome = tool name: 'maven', type: 'maven'
         def mvnCMD = "${mvnHome}/bin/mvn "
         sh "${mvnCMD} clean package"           
        }
       
       
   //3// stage ('Docker Build') {
         
            docker.build('precision')
        }
 //4// stage ('Docker push')
    docker.withRegistry('https://608310603824.dkr.ecr.us-east-2.amazonaws.com/precision', 'ecr:ap-south-1:aws') {
    docker.image('precision').push('latest')
        }
  
 //5// stage ('K8S Deploy'){
                    sh 'kubectl apply -f spring-boot.yaml'
      }
        }
