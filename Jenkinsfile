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
    stage('AB CodeTest'){
        try {
            withMaven(maven:'MyMaven'){
                sh 'mvn test'   
            }
        } finally {
            junit 'target/surefire-reports/*xml'
        }
    }
     stage('AB CoverageChecks'){
        try {
            withMaven(maven:'MyMaven'){
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'   
            }
        } finally {
            cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
        }
    }   
    stage('AB Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}
