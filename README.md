# django-github-action
---
## django 프로젝트 Github Actions CI/CD 삽질 모음

1. secrets.json 생성
   - [Github Actions에서 secrets.json 생성하기](https://velog.io/@hnnynh/Github-Actions%EC%97%90%EC%84%9C-secrets.json-%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0)
   - CI에서는 create-json으로 만들어줬는데 CD에서는 SECRET_JSON을 json 형식으로 만들 방법이 없음
   - ➡ **.env 파일**에서 SECRET_KEY 관리하기
   - EC2에서 Github Action으로 .env파일을 만들어줄 필요가 없다.. .env 파일 수정생기면 직접 수정해주면 된다...
  
2. Job-Chaining
   - 결국 Build ➡ Deploy 이므로 연속적으로 실행되도록 수정

3. python 3.10
   - ubuntu에서는 3.8까지 기본 지원
   - https://www.itsupportwale.com/blog/how-to-upgrade-to-python-3-10-on-ubuntu-18-04-and-20-04-lts/

4. EC2 ```pip install mysqlclient```
   - ```sudo apt-get install python3-dev default-libmysqlclient-dev build-essential```
   - ```sudo apt install pkg-config```
   - ```sudo apt-get install python3.10-dev```

5. python 버전 바꾸기
   - ```sudo update-alternatives --config python3```로 python-3.10으로 바꾸기
   - 기본으로 3.8 venv를 쓰자..

6. AttributeError: module 'dotenv' has no attribute 'read_dotenv'
   - ```pip uninstall django-dotenv``` ```pip uninstall python-dotenv``` -> ```pip install django-dotenv```
   - 그냥 EC2에 secrets.json 저장하고 수동 업데이트 할 예정..

7. nohup timeout
   - https://github.com/appleboy/ssh-action/issues/40

8. nohup.out Permission denied
   - https://structuring.tistory.com/200
   - root에서 ```chmod 777 nohup.out```하고 ubuntu로 돌아오기