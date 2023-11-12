pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                sh 'sqlite3 Employees.db "select * from regions;" ".mode insert" ".output newBackup.sql" ".dump" ".quit"'
                sh 'grep "^INSERT INTO" newBackup.sql > backup.sql'
                sh 'cat newBackup.sql"
                sh 'cat backup.sql"

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
                sh 'sqlite3 Employees.db < sqlite.sql'
            }
        }
        
        stage('Restore Data') {
            steps {
                echo 'Restauración datos'
                sh 'sqlite3 Employees.db ".read backup.sql" "select * from regions;" ".quit"'
            }
        }
    }
}
