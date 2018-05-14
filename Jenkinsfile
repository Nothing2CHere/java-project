properties([pipelineTriggers([githubPush()])])
node('linux') {
git url: 'https://github.com/Nothing2CHere/java-project.git', branch: 'master'
stage('Unit Tests') {
  sh 'ant -f test.xml -v'   // initiate unit tests using ant
  junit 'reports/result.xml'  // create a junit report
}
stage('Build') {
  sh 'ant -f build.xml -v'
}
stage('Deploy') {
  // def output = sh returnStdout: true, script: 'aws ec2 describe-instances | jq .'
  sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://mybucket-browndaniel123/'
}
stage('Report') {
  withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-AWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name HW10'}
  //sh "env"
}
}
