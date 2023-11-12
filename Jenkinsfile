pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                    sh 'sqlite3 Employees.db ".mode insert" ".output backup.sql" ".dump" ".quit"'
                sh 'ls -l'
                sh 'cat backup.sql'
            }
        }
        
        stage('Delete DB') {
            steps {
                echo 'Eliminación del esquema actual'
                sh 'rm Employees.db'
            }
        }
        
        stage('Load Schema') {
            steps {
                echo 'Carga del nuevo esquema'
                sh 'sqlite3 newEmployees.db < sqlite.sql'
                sh 'ls -l'
                sh 'cat newEmployees.db'
            }
        }
        
        stage('Restore Data') {
            steps {
                echo 'Restauración datos'
                sh 'sqlite3 newEmployees.db ".mode insert" ".read backup.sql" ".quit"'
                sh 'ls -l'
                sh 'cat newEmployees.db'
            }
        }
    }
}
