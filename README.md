node('build-in') 
{
   stage('continous dowload') 
                  {
                  git branch: 'nonso', credentialsId: 'opps-user', url: 'https://github.com/ttnwt/webapp.git'
                   } 
        stage('continous build') 
                  {
                  sh 'mvn package'
                 } 
             stage('continous Deployment') 
                  {
                  deploy adapters: [tomcat8(credentialsId: 'bbbb', path: '', url: 'http://172.31.5.164:8080')], contextPath: 'qaenv', war: '**/*.war'
                  } 
              stage('continous test') 
                  {
                  sh ' echo "testing is successful"'
                 }
                 stage('continous delivery') 
                  {
                  deploy adapters: [tomcat8(credentialsId: 'delivery', path: '', url: 'http://172.31.9.205:8080')], contextPath: 'prodenv', war: '**/*.war'
                 }  
}
