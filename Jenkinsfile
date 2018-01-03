#!/usr/bin/env groovy

pipeline {
        agent any

        stages {

                stage('Print values') {
                        steps {
                                echo 'Build path (Terraform): ' + buildPathTerraform
                                echo 'Action: ' + action
                        }
                }

                stage('Terraform apply') {

                        when { 
                                expression {action == 'apply'}
                        }

                        steps {
                build job: 'terraform-apply', 
                                        propagate: true, 
                                        wait: true, 
                                        parameters: [[
                                                $class: 'StringParameterValue', 
                                                name: 'buildPath', 
                                                value: buildPathTerraform]]
                        }
                }

                stage('Terraform destroy') {
                        when {
                                expression {action == 'destroy'}
                        }

                        steps {
                build job: 'terraform-destroy', 
                                        propagate: true, 
                                        wait: true, 
                                        parameters: [[
                                                $class: 'StringParameterValue',
                                                name: 'buildPath',
                                                value: buildPathTerraform]]
                        }
                }

       }
}
