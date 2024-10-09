#!/usr/bin/env groovy
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL
pipeline
{
    agent any
    tools
    {
        maven 'maven'
        jdk 'Amazon Corretto'
    }
    stages
    {
        stage ('Build')
        {
            steps
            {
                echo "Creating New Build"
                sh 'mvn clean install'

            }
        }
        stage ('convert')
        {
            steps
            {
               echo "${env.JOB_NAME}"
               sh """#!/bin/bash
               echo "${env.JOB_NAME}" | cut -d/ -f1


               """
            }
        }
        stage ('Creating and Pushing Docker Image to registry')
        {
            steps
            {
                script
                {
                    def customImage = docker.build("intregrated.azurecr.io/${env.JOB_NAME.toLowerCase()}:${env.BUILD_NUMBER}")
                    sh 'docker login intregrated.azurecr.io -u  -p '
                    customImage.push("${env.BUILD_NUMBER}")
                    customImage.push("latest")
                    //def jobUserId, jobUserName
                    //then somewhere
                    wrap([$class: 'BuildUser']) {
                        env['MYUSER'] = "${BUILD_USER_ID}"

                    }

                }
            }
        }
        stage ('Deploying on UAT')
        {
            steps
            {
                //sh 'ansible-playbook /opt/ansible/playbook/deployment.yaml'
                sh '/opt/ansible/playbook/deploy.sh'
            }
        }

    }
}
