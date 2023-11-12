pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                echo 'Backup de la DB'
                sh '''sqlite3 Employees.db \

        ".mode column" \

        ".headers on" \

        "select * \

           from employees, jobs \

           where jobs.job_id = 1 and employees.job_id = jobs.job_id;"
           '''
            }
        }
        
        stage('Delete DB') {
            steps {
                echo 'Eliminación del esquema actual'
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
