/*
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing,
 * software distributed under the License is distributed on an
 * "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 * KIND, either express or implied.  See the License for the
 * specific language governing permissions and limitations
 * under the License.
 */
/**
 *
 *
 * Jenkins Pipeline configuration.
 *
 */

def labels = 'ubuntu'
def buildJdk = 'JDK 1.8 (latest)'
def buildMvn = 'Maven 3.5.2'
def deploySettings = 'DefaultMavenSettingsProvider.1331204114925'

node(labels) {

    cleanWs()

    stage ('Clone Sources') {
        checkout scm
    }

    stage ('Build') {
        withMaven(
                maven: buildMvn,
                jdk: buildJdk,
                mavenSettingsConfig: deploySettings
        ) {
            sh "mvn clean install -B -U -e -fae -Dmaven.compiler.fork=false"
        } 
    }

    stage ('Deploy') {
        withMaven(
                maven: buildMvn,
                jdk: buildJdk,
                mavenSettingsConfig: deploySettings
        ) {
            sh "mvn deploy -Dmaven.test.skip=true -B -U -e -fae -Dmaven.compiler.fork=false"
        }
    }
}
