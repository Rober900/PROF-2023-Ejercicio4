pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                    sh '''
                        sqlite3 Employees.db ".mode insert" ".output backup.sql" "select * from jobs;" "select * from employees;" "select * from dependents;" "select * from departments;" "select * from regions;" "select * from countries;" "select * from locations;" ".quit"
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
