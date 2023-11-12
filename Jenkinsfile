pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                sh 'sqlite3 Employees.db .dump > backup.sql'
                sh 'ls -l'
            }
        }
        
        stage('Delete DB') {
            steps {
                echo 'Eliminación del esquema actual'
                sh 'sqlite3 DROP DATABASE Employees.db'
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
