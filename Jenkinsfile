//macevedo 20220517
pipeline {
    agent any
    //tools {
    //    gradle "gradle_742"
    //}
        stages {
            stage('checkout') {
                steps {
                    git branch: 'master', credentialsId: 'azuredevops-macevedo', url: 'https://valorunico@dev.azure.com/valorunico/Idemia_INT_P_SRCeI/_git/AppNoVidentes_IOS_SRCeI'
                    echo '###########Carga del repositorio##########################'
                }
            }
            stage('SonarCloud') {
                environment {
                    SCANNER_HOME = tool 'sonarqubescanner'
                    ORGANIZATION = "valorunico"
                    PROJECT_NAME = "AppNoVidentes_IOS_SRCeI"
                }
                steps {
                    echo '######analisis estatico de codigo con sonar qube#########'
                    withSonarQubeEnv ('SonarCloudVunic') {
                        sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                        -Dsonar.projectKey=$PROJECT_NAME \
                        -Dsonar.sources=. \
                        -Dsonar.c.file.suffixes=- \
                        -Dsonar.cpp.file.suffixes=- \
                        -Dsonar.objc.file.suffixes=- \
                        -Dsonar.qualitygate.wait=true"
                    }
                }
            }
        }

}
