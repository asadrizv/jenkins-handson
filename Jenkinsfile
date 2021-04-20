pipeline {
    agent any
    parameters {
        string(defaultValue: 'default', name: 'skip_checks', trim: false)
        string(defaultValue: 'default', name: 'enable_checks', trim: false)
        string(defaultValue: '', name: 'args', trim: true)
        string(defaultValue: '', name: 'kubernetes_manifest', trim: false)
        string(defaultValue: '', name: 'CHKK_ACCESS_TOKEN', trim: false)
    }
    stages {
        stage("Chkk") {
            steps {
               echo "${params.enable_checks}"
               echo "${params.skip_checks}"
               sh '''#!/bin/bash
               curl -Lo chkk https://chkk-artifacts-downloads.s3.amazonaws.com/dl/v0.0.1/chkk-darwin-amd64;
               export CHKK_ACCESS_TOKEN=${CHKK_ACCESS_TOKEN};
               chmod +x chkk;
               ./chkk -f ${kubernetes_manifest}  -r ${enable_checks} -s ${skip_checks}
               '''
               
            }
        }
        
    }   
}
