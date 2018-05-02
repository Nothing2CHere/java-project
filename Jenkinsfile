properties([pipelineTriggers([githubPush()])])
node('linux') {
git url: 'https://github.com/Nothing2CHere/java-project.git', branch: 'master'
stage('Unit Tests') {
  sh 'ant -f test.xml -v'
  junit 'reports/result.xml'
}
stage('Build') {
  sh 'ant -f build.xml -v'
}
stage('Deploy') {
  // def output = sh returnStdout: true, script: 'aws ec2 describe-instances | jq .'
  sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://mybucket-browndaniel123/'
}
stage('Report') {
  withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'a242a259-1916-44af-adf2-00f546565b3b', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name HW10'}
  //sh "env"
}
}
