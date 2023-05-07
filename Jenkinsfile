pipeline{
    agent{
        label{
        label "built-in"
        customWorkspace "/mnt/project"
    }
    }
    stages{
        stage ("git-clone"){
            steps{
                sh "rm -rf *"
                sh "git clone https://github.com/Shantanumajan6/game-of-life.git"
                sh "yum install maven -y"
            }
        }
        stage ("maven-compile") {
            steps{
                dir ("/mnt/project/game-of-life"){
                    sh "mvn clean install"
                }
            }
        }
    stage ("deploy"){
        steps{
            dir ("/mnt/project/game-of-life/gameoflife-web/target") {
            //sh "cd /mnt/project/game-of-life/gameoflife-web/target"
            sh "scp -i '/mnt/test.pem' -o StrictHostKeyChecking=no gameoflife.war ec2-user@172.31.38.24:/mnt/servers/apache-tomcat-9.0.74/webapps"
        }
        }
    }
    }
}
