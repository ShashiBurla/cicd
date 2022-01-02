pipeline {
agent {
label 'Build-server'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/java-project/spring ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/java-project/spring; sudo docker build -t spring . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/java-project/spring ; sudo  docker login -ushashi406 -pShashi@123 "
        sh "cd /home/ubuntu/workspace/java-project/spring ; sudo docker tag spring shashi406/spring "
        sh "cd /home/ubuntu/workspace/java-project/spring ; sudo docker push shashi406/spring  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node (' Ansible-server') {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}
    
    
}
