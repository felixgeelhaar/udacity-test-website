pipeline {
    agent any
    stages {
       stage('Release') {
             steps {
                 withAWS(region:'eu-central-1', credentials:'aws-static') {
                  sh 'echo "Uploading content to AWS S3"'
                  s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, includePathPattern:'*', bucket:'felixgeelhaar.com')
                  
                  sh 'echo "Invalidating Cloudfront cache"'
                  cfInvalidate(distribution: "E21JQVVQL54JYX", paths: ['/*'], waitForCompletion: true)
                 }
             }
        }
    }
}
