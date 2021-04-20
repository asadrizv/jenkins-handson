pipeline {
    agent any
    parameters {
        string(defaultValue: 'default', name: 'skip-checks', trim: true)
        string(defaultValue: 'default', name: 'enable-checks', trim: true)
        string(defaultValue: '', name: 'args', trim: true)
        string(defaultValue: 'kubernetes-manifest', name: 'kubernetes-manifest', trim: true)
    }
    stages {
        stage("Chkk") {
            steps {
               sh '''#!/bin/bash
              curl -Lo chkk https://chkk-artifacts-downloads.s3.amazonaws.com/dl/v0.0.1/chkk-darwin-amd64;
               export CHKK_ACCESS_TOKEN=$CHKK_ACCESS_TOKEN;
               chmod +x chkk;
               ./chkk --file ${kubernetes-manifest} --run-check ${enable-checks} --skip-check ${skip-checks}
               '''
            }
        }
        
    }   
}
