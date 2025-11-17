pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo "📦 Meng-clone repository..."
                checkout scm
            }
        }

        stage('Validate Files') {
            steps {
                echo "📁 Validating required files..."
                sh '''
                    echo "List semua file:"
                    ls -la

                    if [ -f index.html ]; then
                        echo "✅ SUCCESS: index.html ditemukan"
                    else
                        echo "❌ ERROR: index.html tidak ada!"
                        exit 1
                    fi

                    if [ -f css/style.css ]; then
                        echo "✅ SUCCESS: css/style.css ditemukan"
                    else
                        echo "❌ ERROR: css/style.css tidak ada!"
                        exit 1
                    fi
                '''
            }
        }

        stage('Build') {
            steps {
                echo "🔧 Build sederhana..."
                sh '''
                    echo "Build timestamp: $(date)" > build-info.txt
                    echo "Build selesai."
                '''
            }
        }

        stage('Simple Deploy') {
            steps {
                echo "🚀 Deploying files..."
                sh '''
                    mkdir -p deployed

                    echo "📂 Copy semua file kecuali folder deployed..."
                    for item in *; do
                        if [ "$item" != "deployed" ]; then
                            cp -r "$item" deployed/
                        fi
                    done

                    echo "Deployed at: $(date)" > deployed/deploy-info.txt

                    echo "🎉 Deployment sukses!"
                '''
            }
        }
    }

    post {
        success {
            echo "✨ Pipeline berhasil!"
        }
        failure {
            echo "💥 Pipeline gagal!"
        }
    }
}
