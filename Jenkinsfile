def bucket = 'lambdaspace'
def functionName = 'LambdaHello'
def region = 'us-east-1'

node('master'){
    stage('Checkout'){
        checkout scm
    }
    
    stage('Build'){
        sh 'mvn clean package'
    }
    
    stage('Push'){
        sh "aws s3 cp target/demo-1.0.0.jar s3://${bucket}"
    }
    
    stage('Deploy'){
        sh "aws lambda update-function-code --function-name ${functionName} \
                --s3-bucket ${bucket} \
                --s3-key target/demo-1.0.0.jar \
                --region ${region}"
    }
    
    stage('Publish') {
        sh "aws lambda publish-version --function-name ${functionName} \
                    --region ${region}"
    }
}