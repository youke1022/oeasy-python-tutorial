pipeline {
    agent any
    
    stages {
        stage('启动容器并挂载项目') {
            steps {
                script {
                    echo "创建并启动dixiacheng容器..."
                    // Windows宿主机使用bat命令
                    bat '''
                        docker run -d ^
                            --name dixiacheng ^
                            -v %WORKSPACE%:/app ^
                            python:3.9-slim ^
                            tail -f /dev/null
                    '''
                    echo "容器启动成功，项目已挂载到/app目录"
                }
            }
        }
        
        stage('执行游戏脚本') {
            steps {
                script {
                    echo "进入容器并执行游戏..."
                    // 严格按照要求传递输入序列：a→100→1
                    bat 'docker exec dixiacheng sh -c \'cd /app/samples/000005 && echo -e "a\\n100\\n1\\n" | python game.py\''
                }
            }
        }
    }
}
