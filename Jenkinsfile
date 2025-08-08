pipeline {
    agent any
    
    stages {
        stage('拉取GitHub代码') {
            steps {
                script {
                    echo "从GitHub拉取代码..."
                    bat '''
                        git clone https://github.com/youke1022/oeasy-python-tutorial %WORKSPACE%
                    '''
                    echo "代码拉取完成"
                }
            }
        }
        
        stage('启动容器并挂载项目') {
            steps {
                script {
                    echo "创建并启动dixiacheng容器..."
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
                    // 修复Windows bat命令的引号转义问题
                    bat "docker exec dixiacheng sh -c \"cd /app/samples/000005 && echo -e 'a\\n100\\n1\\n' | python game.py\""
                }
            }
        }
    }
}
