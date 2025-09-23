pipeline {
    agent any // 使用任何可用的代理节点
    
    environment {
        // 定义部署目录，请根据您的服务器实际情况修改
        DEPLOY_PATH = '/var/www/html'
    }
    
    stages {
        stage('拉取代码') {
            steps {
                checkout scm // 从配置的 SCM 拉取代码
                echo '代码拉取完成'
            }
        }
        
        stage('部署到服务器') {
            steps {
                sh """
                    # 创建部署目录（如果不存在）
                    sudo mkdir -p ${DEPLOY_PATH}
                    
                    # 复制 HTML 文件到部署目录
                    sudo cp -f index.html ${DEPLOY_PATH}/index.html
                    
                    # 调整权限（根据需要）
                    sudo chmod 644 ${DEPLOY_PATH}/index.html
                    
                    echo '网站已成功部署到服务器'
                """
            }
        }
    }
    
    post {
        success {
            echo '✅ 流水线执行成功！网站已更新。'
        }
        failure {
            echo '❌ 流水线执行失败，请检查错误。'
        }
    }
}