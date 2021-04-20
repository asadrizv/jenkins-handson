pipeline {
    agent any
    parameters {
        string(defaultValue: 'default', name: 'skip-checks', trim: false)
        string(defaultValue: 'default', name: 'enable-checks', trim: false)
        string(defaultValue: '', name: 'args', trim: true)
        string(defaultValue: '', name: 'kubernetes-manifest', trim: false)
    }
    stages {
        stage("Chkk") {
            steps {
               sh '''#!/bin/bash
               curl -Lo chkk https://chkk-artifacts-downloads.s3.amazonaws.com/dl/v0.0.1/chkk-darwin-amd64;
               export CHKK_ACCESS_TOKEN=$CHKK_ACCESS_TOKEN;
               chmod +x chkk;
               echo ${kubernetes-manifest}
               ./chkk --file kubernetes-manifest.yaml --run-check ${params.enable-checks} --skip-check ${param.skip-checks}
               '''
            }
        }
        
    }   
}
