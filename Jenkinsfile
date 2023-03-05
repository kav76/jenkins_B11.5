pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                // Get code from a GitHub repository
                git url: 'https://github.com/kav76/jenkins_B11.5.git', branch: 'main'
            }
        }
        stage("GetSQLRequest"){
            steps {
                // Make single line sql select from readed file
                script {
                    def sqlFile = readFile 'sql-req.sql'
                    def lines = sqlFile.readLines()
                    def sqlLine = ''
                    for (line in lines) {
                        sqlLine = sqlLine + line
                    }
                    env.sqlLine = sqlLine
                }
                // Echo to console slq request for debug
                echo "SQL request: ${env.sqlLine}"
                // Run MySQL client with 
                sh "mysql --host=mysql-rfam-public.ebi.ac.uk --port=4497 --user=rfamro --database=Rfam --execute='${env.sqlLine}'"
            }
        }
    }
    
}
