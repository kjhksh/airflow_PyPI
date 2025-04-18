- 데이터베이스 백엔드 설정 

CREATE DATABASE airflow_db;
CREATE USER airflow_user WITH PASSWORD 'airflow_pass';
GRANT ALL PRIVILEGES ON DATABASE airflow_db TO airflow_user;
GRANT ALL ON SCHEMA public TO airflow_user;


- AIRFLOW 설치

mkdir airflow_tutorial

mkdir -p ./dags ./logs ./plugins ./config
mkdir -p ./data ./data/oracle ./data/mssql ./data/postgres

<!-- 가상환성 설정 -->
python3 -m venv py_env
source py_env/bin/activate  /* deactivate  */


// export AIRFLOW_HOME=~/airflow
//export AIRFLOW_HOME=/home/kim/airflow_tutorial
export AIRFLOW_HOME=~/airflow_tutorial
echo $AIRFLOW_HOME

AIRFLOW_VERSION=2.10.5

PYTHON_VERSION="$(python -c 'import sys; print(f"{sys.version_info.major}.{sys.version_info.minor}")')"

CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

pip install "apache-airflow[celery]==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
pip install "apache-airflow[celery, postgres]==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"


<!-- //pip install 'apache-airflow==2.10.5' --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.10.5/constraints-3.9.txt"

pip install 'apache-airflow==2.10.5' --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.10.5/constraints-3.10.txt" -->

airflow standalone

// Airflow 설정:
sql_alchemy_conn 설정: DB 설정
  sql_alchemy_conn = postgresql+psycopg2://airflow_user:airflow_pass@localhost:5432/airflow_db

# executor = SequentialExecutor  # 필요에 따라 다른 Executor로 변경
executor = LocalExecutor

// 리눅스 패키지 설치/업데이트:
sudo apt-get update && sudo apt-get install -y pkg-config libmysqlclient-dev


// 패키지 설치
pip list | grep amazon
pip install -r requirements.txt


// airflow db 초기화
airflow db init
airflow db migrate

// airflow 관리자 생성
airflow users create \
  --username admin \
  --firstname FIRST_NAME \
  --lastname LAST_NAME \
  --role Admin \
  --email admin@example.org

// airflow webserver 실행
source py_env/bin/activate
export AIRFLOW_HOME=~/airflow_tutorial
airflow webserver -p 8080


//AIRFLOW acheduler 설정
source py_env/bin/activate
export AIRFLOW_HOME=~/airflow_tutorial
airflow scheduler


airflow webserver -D
airflow scheduler -D

pkill -f "airflow webserver"
pkill -f "airflow scheduler"

