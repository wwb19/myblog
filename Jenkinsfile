pipeline {
  agent {
    node {
      label 'Jenkins_slave_hexo'
    }
  }
 /*triggers {
      githubPush()
 }*/
 options{
         /*disableConcurrentBuilds()*/
         skipDefaultCheckout()
         timestamps()
    }
  environment { 
    def HTTP_PROXY="http://192.168.2.118:10080"
    def HTTPS_PROXY="http://192.168.2.118:10080"
    def all_proxy="socks5://192.168.2.118:10080"
	  
    GITHUB_TOKEN=credentials('98f28b74-a03f-432e-a2a9-18cf52150e4a')
    
  }
  stages {
  stage('Init') {
	steps{
		script{
			println "welcome to Nick learn"
			sh 'printenv'
		}
	}
	}
  stage('checkout') {
	steps{
		script{
		container('hexo') {
		  sh 'pwd'
		  sh 'ls -lrt'
		  sh 'echo ---------------------'
		  sh 'git clone https://github.com/wwb19/myblog.git'
		}
	}
    	}	
    }
    
    stage('hexo') {
		steps{
			script{
    			container('hexo') {
    			  dir('/home/jenkins/agent/workspace/hexo-myblog/myblog'){
				  sh 'pwd'
				  sh 'ls -lrt'
				  sh 'rm -rf .deploy_git'
				  sh 'sed -i "s/__GITHUB_TOKEN__/${GITHUB_TOKEN}/" _config.yml'
				  sh 'hexo generate'
				  sh 'hexo deploy'
    			  }
    			}
		    }
	    }
    }
  }
}
