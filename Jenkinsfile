pipeline {
    environment {
        DEPLOY = "${env.BRANCH_NAME == "fabr" || env.BRANCH_NAME == "fabr" ? "true" : "true"}"
        NAME = "${env.BRANCH_NAME == "master" ? "example" : "example-staging"}"
        DOMAIN = 'localhost'
        dockerImage = ''
        REGISTRY = 'fabr9013/bpsptwso2'
        registryCredential = '7030bf22-a808-4bd4-99e8-df7f13619bf1'
        chartsName="vclusterwekiitk"
        namespace="wekii"
    }
  agent {
    kubernetes {
      cloud 'vcluster-wekii'
      inheritFrom 'wso2mi'
      idleMinutes 5  // how long the pod will live after no jobs have run on it
      yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project 
      defaultContainer 'maven'  // define a default container if more than a few stages use it, will default to jnlp container
    }
  }
      stages {

          
        stage('Deploy WP-wekiitk to K8S') {	
            steps {
                echo 'Deploy to K8s custom pod WSO2MI CE....'
                /* Funciona con el plugin de Kubernetes deployment de Azure -Actualmente tiene un bug-
                   script {
          		kubernetesDeploy (configs: 'deployment.yaml',kubeconfigId: 'kubeconfdigoce')
        		    }*/
        		 container('helm'){    
        		    //workaround=> use helm hasta que actualicen el plugin kubernetesDeploy
                //Despliego Ingress usando nginx
                //
        		    //sh 'helm repo add nginx-stable https://helm.nginx.com/stable'
        		    //sh 'helm repo update'
        		    //sh 'helm install nginx-ingress-${chartsName} nginx-stable/nginx-ingress --set controller.publishService.enabled=true,controller.hostNetwork=true,controller.service.type="" --namespace wso2mi'
        		    
                     //Despliego el servicio de WP- wekiitk
                     //Deploy
                //sh 'helm install ${chartsName} ./helmscharts/${chartsName} --namespace ${namespace}'
                     //TEST
        		    sh 'helm install ${chartsName} ./helmscharts/${chartsName} --namespace ${namespace} --dry-run --debug'
                 }
            }
         }
          
     }
}
