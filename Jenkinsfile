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
  withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAIKYKLDYJCIQH6G7Q', credentialsId: '', secretKeyVariable: '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']]) {
    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name HW10'
  }
//sh "env"
}
}
