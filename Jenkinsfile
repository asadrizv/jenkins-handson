def getOs(){
    String osname = System.getProperty('os.name');
    if (osname.startsWith('Windows'))
        return 'windows';
    else if (osname.startsWith('Mac'))
        return 'macosx';
    else if (osname.contains('nux'))
        return 'linux';
    else
        throw new Exception("Unsupported os: ${osname}");
}
pipeline {
    agent any
    parameters {
        string(defaultValue: 'default', name: 'skip_checks', trim: false)
        string(defaultValue: 'default', name: 'enable_checks', trim: false)
        string(defaultValue: '', name: 'args', trim: true)
        string(defaultValue: '', name: 'kubernetes_manifest', trim: false)
    }
    environment {
    CHKK_ACCESS_TOKEN = credentials("CHKK_ACCESS_TOKEN")
    }
    stages {
        stage("Chkk") {
            steps {
                if(getOs() == "macosx")
                {
                     sh '''#!/bin/bash
                     curl -Lo chkk https://chkk-artifacts-downloads.s3.amazonaws.com/dl/v0.0.1/chkk-darwin-amd64;
                     export CHKK_ACCESS_TOKEN=$CHKK_ACCESS_TOKEN;
                     chmod +x chkk;
                     ./chkk -f ${kubernetes_manifest}  -r ${enable_checks} -s ${skip_checks}
                     '''
                }
                else
                {
                     sh '''#!/bin/bash
                     curl -Lo chkk https://chkk-artifacts-downloads.s3.amazonaws.com/dl/v0.0.1/chkk-linux-amd64;
                     export CHKK_ACCESS_TOKEN=$CHKK_ACCESS_TOKEN;
                     chmod +x chkk;
                     ./chkk -f ${kubernetes_manifest}  -r ${enable_checks} -s ${skip_checks}
                     '''      
                }          
               
            }
        }
        
    }   
}
