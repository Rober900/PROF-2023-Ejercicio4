pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                sh 'sqlite3 Employees.db ".mode insert" ".output newBackup.sql" ".dump" ".quit"'
                sh 'grep "^INSERT INTO" newBackup.sql | sed "s/^INSERT INTO/INSERT INTO new_table_name/" > backup.sql'
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
                sh 'sqlite3 Employees.db < sqlite.sql'
                sh 'ls -l'
                sh 'cat Employees.db'
            }
        }
        
        stage('Restore Data') {
            steps {
                echo 'Restauración datos'
                sh 'sqlite3 Employees.db ".mode insert" ".read backup.sql" ".quit"'
                sh 'ls -l'
                sh 'cat Employees.db'
            }
        }
    }
}
