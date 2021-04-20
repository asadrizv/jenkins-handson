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
               echo "${ENABLE-CHECKS}"
               echo "${SKIP-CHECKS}"
               sh '''#!/bin/bash
               curl -Lo chkk https://chkk-artifacts-downloads.s3.amazonaws.com/dl/v0.0.1/chkk-darwin-amd64;
               export CHKK_ACCESS_TOKEN=$CHKK_ACCESS_TOKEN;
               chmod +x chkk;
               ./chkk --file kubernetes-manifest.yaml
               '''
            }
        }
        
    }   
}
