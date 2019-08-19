#!/usr/bin/env groovy
import java.net.URL

node{
    stage('Git Checkout'){
        git 'https://github.com/edureka-git/DevOpsClassCodes.git'
    }
    stage('AB Compile'){
        withMaven(maven:'MyMaven'){
            sh 'mvn compile'
        }
    }
    stage('AB CodeReview'){
        try {
            withMaven(maven:'MyMaven'){
                sh 'mvn pmd:pmd'   
            }
        } finally {
            pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
        }
    }
        
    stage('AB Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}
