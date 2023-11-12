pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                    sh '''
                        sqlite3 Employees.db ".mode insert" ".output backup.sql" "SELECT 'SELECT * FROM ' || name || ';' FROM sqlite_master WHERE type = 'table';" ".quit"
                    '''
                sh 'ls -l'
                sh 'cat backup.sql'
            }
        }
        
        stage('Delete DB') {
            steps {
                echo 'Eliminación del esquema actual'
                sh 'sqlite3 DROP SCHEMA Employees.db'
            }
        }
        
        stage('Load Schema') {
            steps {
                echo 'Carga del nuevo esquema'
            }
        }
        
        stage('Restore Data') {
            steps {
                echo 'Restauración datos'
            }
        }
    }
}
