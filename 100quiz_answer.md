
# 1 - 10

1.

action - workflow - job - step

a: workflow-job-step-action


2.

on:
    workflow_dispatch:
    pull_request:
        types:
            - opened


3.

  stpe은 순서대로 실행이 되는데, step2가 실패하면 hello를 입력하세요 인데, 이미 step1에서 오류가 발생하면 작업을 멈추라고 했기에 실행되지 않음


a: step 2의 if: failure()은 이전 스텝이 실패하면 실행하는 것 이기에. step 1: exit 1 --> step 2가 실행이 됨

4.

needs를 사용하는 이유는 병렬로 연결되어서 실행되는 job의 순서를 정하기 위해

의존관계를 정하기 위해서 사용

5.

stpes:
    - id: my-step
      run: echo "color=green" >> "mycolor"

    - run: echo "{{ step.my-step.outputs.mycolor }}"

a:
steps:
    - id: my-step
      run: echo "color=green" >> "$GITHUB_OUTPUT"

    - run: echo "{{ step.my-step.outputs.color }}"

6.

job-1 print: Hello Peter
job-2 print: Hello <UNSET>

7.

secrets: DB 비밀번호, API 키
variable : 서버 주소, 서버 포트 번호


8.

features branch에서 push 될때, src 의 어떤 ts 확장자 파일이 PR 요청이 왔을때, 직접 workflow 실행할때


9.

env:
    MY_VAR: hello

jobs:
    job-1:
        runs-on: ubuntu-24.04
        steps:
            - run: echo "$MY_VAR"

10.

조합은 총 2 x 3 = 6, 6개이다. exclude로 5개만 싱행 된다.

# 11 - 20

11.

run: |
은 하나의 스텝으로 작동한다. 주로 관련있는 작업을 함께 적어두며 코드 하나가 오류가 나면 step 전체가 멈춘다.

각각 - run:
은 개별의 스텝이다. 다른 작업들을 할때, 주로 사용하며 로그에서도 구분되어 진다.

12.

consumer Job이 실행되기 위해서는 needs: producer job이 요구된다.

a:
jobs:
  producer:
    runs-on: ubuntu-24.04
    steps:
      - id: set-value
        outputs:
            color: ${{ steps.set-value.outputs.color }}
        run: echo "color=green" >> "$GITHUB_OUTPUT"

  consumer:
    runs-on: ubuntu-24.04
    needs: producer
    steps:
      - run: echo "color is ${{ needs.producer.outputs.color }}"

13.

jobs:
    job-1:
    job-2:
    job-3:
        needs: [job-1, job-2]
    job-4:
        needs: [job-2, job-3]

14.

그렇게 되면 이미 cache-hit, 즉 이미 cache된 데이터가 있기에 npm의 다운로드를 하지 않는다! npm ci 를 싱행하지 않음


15.

secret은 외부에 공개되지 않아야 하는 정보로, 비밀번호, API kEY 등이 해당되며 github actions에서 자동으로 masking을 해준다.

그에 반해 environment는 환경에 관한 정보로, variable에 속한다. 마스킹 되지 아니하며 이 또한 github actions에서 관리 가능하다.  xxxxx

a:
environment: staging, production 같은 배포 환경 그룹. 각 환경마다 다른 secret/variable을 가질 수 있다.

16.

with의 역할은 파라미터다. 즉 acitons/upload-artifact action에 필요한 정보를 넘겨주는데, 아마 파일이 있는 위치인듯 함.

17.

main branch에서 push 했을때, src안에 파일이 변경되어 push 했을떄, 하나는 모르겠는데?

a: push의 brach, paths 둘다 만족해야 실행되어진다.

18.

A. Artifact는 파일을 저장. GITHUb_OUTPUT은 텍스트 값을 저장

19.

jobs:
    job-1:
        runs-on: ubuntu-24.04
        permission:
            pull-requests: write
        steps:
            - run: gh pr edit 1 --add-label "bug"
              env:
                GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}


20.

1) 관리가 용이함. 자동으로 만료되기에 기간에 대한 관리가 쉽다.
2) 유츌될 가능성이 적기 때문에, 보안상 더 안전함.

# 21 - 30

21.

secret.GITHUB_TOKEN은 github에서 발급해준다.

- Github에서 workflow 실행할 떄 자동으로 발급 workflow가 끝나면 자동 만료

22.

environment는 선언하는 환경에 따라 secret 등을 다르게 설정할 수 있기에 production으로 선언한다면 그에 맞는 secret과 variable을 사용가능함

23.

1) job-1, job-2는 동시에 실행
2) job-3, job-4가 동시 실행


a:
1) job-1, job-2 동시 실행
2) job-1 끝나면 job-3 실행
   job-1, job-2가 끝나면 job-3 실행

시간이 얼마나 걸릴지 모르기에


24.

artifact는 파일을 저장하는 요소로써. file, 결과.txt, app.zip 같은 것으로 파일 저장 및 전달을 하기 위해서 존재

25.

- uses: actions/cache@v4
  with:
    path: node_modules
    key: npm-${{ hashFiles('package-lock.json') }}

캐시가 있으면 cache-hit= 'true'
캐시가 없으면 cache-hit= 'false', cache-hit != 'true'

26.

A: checkout의 4버전을 사용함. 코드 소유주가 새로운 커밋을 하거나, 수정하면 그대로 반영되어벎

B: checkout의 커밋 해시에 맞는 버전을 사용하기에, 변화에 대해 자유로움

SHA

27.

Composite Action:
자주 사용할 것같은 step들을 묶어서 하나의 action으로 만드는 것.

Reusable Workflow:
내가 만든 어떠한 workflow 전체를 다시 참조해서 사용하는 것. 

28.

./services/api 안에 있는 Taskfile.yaml를 사용하기 위해?

a:

Taskfile만을 위한 것이 아니라

working-directory는 이 경로에서 명령어를 실행해!, 해당 폴더 이동 후 run 실행

즉, task test을 ./service/api 폴더 안에서 실행하는 것. Taskfile이 없어도 된다는 의미


29,

****
SECRET is password123

a:

*****

SECRET is *****

한번 masking을 추가하면 전부 마스킹됨!

30.

jobs:
    deploy:
        runs-on:ubuntu-24.04
        permissions:
            id-token: write

# 31 ~ 40

31.

