Github Actions QUIZ


# 퀴즈 1~10번 📝

1번 workflow를 구성하는 요소를 큰 것부터 작은 순서로 나열해봐요.
step / workflow / action / job
답 :

2번 다음 코드의 오타를 찾아봐요.
on:
  workflow_dispach:
  pull_request:
    types:
      - opened
답 :

3번 아래 코드에서 step 2는 언제 실행돼요?
steps:
  - run: exit 1
  - name: step 2
    if: failure()
    run: echo "hello"
답 :

4번 needs를 사용하는 이유가 뭐야?
답 :

5번 아래 빈칸을 채워봐요.
steps:
  - id: my-step
    run: echo "color=____" >> "____"

  - run: echo "${{ steps.my-step.outputs.____ }}"
답 :

6번 아래 코드 실행 결과는?
env:
  GREETING: Hello

jobs:
  job-1:
    env:
      NAME: Peter
    steps:
      - run: echo "$GREETING $NAME"

  job-2:
    steps:
      - run: echo "$GREETING ${NAME:-<UNSET>}"
답 :

7번 다음 중 secret을 사용해야 하는 것, variable을 사용해야 하는 것을 구분해봐요.
DB 비밀번호
서버 포트 번호
AWS API 키
서버 주소
답 :

8번 아래 코드가 실행되는 조건은?
on:
  push:
    branches:
      - "feature/*"
  pull_request:
    paths:
      - "src/**/*.ts"
  workflow_dispatch:
답 :

9번 아래 코드에서 잘못된 부분을 찾아봐요.
env:
  MY_VAR=hello

jobs:
  job-1:
    steps:
      - echo "$MY_VAR"
답 :

10번 Matrix 조합은 총 몇 개이고, exclude 후에는 몇 개가 실행돼요?
strategy:
  matrix:
    os: [ubuntu, windows]
    node: [16, 18, 20]
    exclude:
      - os: windows
        node: 16
답 :


# 퀴즈 11~20번 📝

11번 run: | 와 각각 - run: 의 차이가 뭐야?
답 :

12번 아래 코드에서 consumer Job이 실행되려면 무엇이 필요해요?
yaml

jobs:
  producer:
    runs-on: ubuntu-24.04
    steps:
      - id: set-value
        run: echo "color=green" >> "$GITHUB_OUTPUT"

  consumer:
    runs-on: ubuntu-24.04
    needs: producer
    steps:
      - run: echo "color is ${{ needs.producer.outputs.color }}"
답 :

13번 아래 빈칸을 채워봐요.
yaml

jobs:
  job-1:
  job-2:
  job-3:
    needs: [____, ____]   # job-1과 job-2가 끝나야 실행
  job-4:
    needs: [____, ____]   # job-2와 job-3이 끝나야 실행
답 :

14번 아래 코드에서 cache-hit가 true인 경우 어떤 일이 발생해요?
yaml

steps:
  - id: my-cache
    uses: actions/cache@v4
    with:
      path: node_modules
      key: npm-${{ hashFiles('package-lock.json') }}

  - name: Install dependencies
    if: steps.my-cache.outputs.cache-hit != 'true'
    run: npm ci
답 :

15번 secret과 environment의 차이가 뭐야?
답 :

16번 아래 코드에서 with의 역할은?
yaml

- uses: actions/upload-artifact@v4
  with:
    name: my-artifact
    path: ./output
답 :

17번 아래 코드가 실행되는 조건을 말해봐요.
yaml

on:
  push:
    branches:
      - main
    paths:
      - "src/**"
답 :

18번 다음 중 Artifact와 GITHUB_OUTPUT의 차이가 뭐야?
A. Artifact는 파일을 저장, GITHUB_OUTPUT은 텍스트 값을 저장
B. 둘 다 파일을 저장
C. Artifact는 텍스트 값, GITHUB_OUTPUT은 파일을 저장
D. 둘 다 텍스트 값을 저장
답 :

19번 아래 코드에서 잘못된 부분을 찾아봐요.
yaml

jobs:
  job-1:
    runs-on: ubuntu-24.04
    permissions:
      pull-requests: read
    steps:
      - run: gh pr edit 1 --add-label "bug"
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
답 :

20번 OIDC 인증 방식이 Static Key보다 좋은 이유 2가지를 말해봐요.
답 :

# 퀴즈 21~30번 📝

21번 secrets.GITHUB_TOKEN 은 누가 발급해주는거야?
답 :

22번 아래 코드에서 environment: production 을 선언하면 어떤 효과가 있어?
yaml

jobs:
  deploy:
    runs-on: ubuntu-24.04
    environment: production
    steps:
      - run: echo "deploying..."
답 :

23번 아래 코드의 실행 순서를 말해봐요.
yaml

jobs:
  job-1:
    runs-on: ubuntu-24.04
  job-2:
    runs-on: ubuntu-24.04
  job-3:
    needs: job-1
  job-4:
    needs: [job-1, job-2]
답 :

24번 Artifact를 사용하는 이유가 뭐야?
답 :

25번 아래 빈칸을 채워봐요.
yaml

```
- uses: actions/cache@v4
  with:
    path: node_modules
    key: npm-${{ hashFiles('package-lock.json') }}

# 캐시가 있으면 cache-hit = ____
# 캐시가 없으면 cache-hit = ____

```

답 :

26번 아래 두 코드의 차이점은?
yaml

```
# A
uses: actions/checkout@v4

# B
uses: actions/checkout@ff7abcd0c3c05ccf6adc123a8cd1fd4fb30fb493
å
```

답 :

27번 Composite Action과 Reusable Workflow의 차이점은?
답 :

28번 아래 코드에서 working-directory의 역할은?
yaml

steps:
  - name: Run tests
    working-directory: ./services/api
    run: task test

답 :

29번 아래 코드가 출력하는 결과는?
yaml

steps:
  - name: Mask value
    env:
      SECRET: "password123"
    run: |
      echo "::add-mask::$SECRET"
      echo "SECRET is $SECRET"
답 :

30번 Static Key 방식 대신 OIDC를 사용할 때 permissions에 반드시 추가해야 하는 것은?
yaml

jobs:
  deploy:
    runs-on: ubuntu-24.04
    permissions:
      ____: ____
답 :


# 퀴즈 31~40번 📝

31번 아래 코드에서 if: 조건이 하는 역할은?
yaml

jobs:
  deploy:
    runs-on: ubuntu-24.04
    steps:
      - name: Deploy to production
        if: github.ref == 'refs/heads/main'
        run: echo "deploying to production"
답 :

32번 아래 코드에서 fail-fast: false 를 설정하면 어떻게 돼?
yaml

strategy:
  fail-fast: false
  matrix:
    node: [16, 18, 20]
답 :

33번 workflow_dispatch 와 workflow_call 의 차이점은?
답 :

34번 아래 코드에서 잘못된 부분을 찾아봐요.
yaml

jobs:
  producer:
    runs-on: ubuntu-24.04
    steps:
      - id: set-color
        run: echo "color=green" >> "$GITHUB_OUTPUT"

  consumer:
    runs-on: ubuntu-24.04
    needs: producer
    steps:
      - run: echo "${{ needs.producer.outputs.color }}"
답 :

35번 아래 코드에서 schedule 이벤트는 한국 시간으로 몇 시에 실행돼?
yaml

on:
  schedule:
    - cron: "0 3 * * *"
답 :

36번 continue-on-error: true 는 어떤 역할을 해?
yaml

jobs:
  job-1:
    runs-on: ubuntu-24.04
    continue-on-error: true
    steps:
      - run: exit 1
답 :

37번 아래 두 가지 secrets 전달 방식의 차이점은?
yaml

```

# A
secrets: inherit

# B
secrets:
  MY_SECRET: ${{ secrets.MY_SECRET }}

```

답 :

38번 아래 코드에서 GITHUB_STEP_SUMMARY 의 역할은?
yaml

steps:
  - run: |
      echo "### 배포 완료 🚀" >> $GITHUB_STEP_SUMMARY
      echo "- 버전: 1.0.0" >> $GITHUB_STEP_SUMMARY
답 :

39번 Lint가 뭐야? 왜 필요해?
답 :

40번 아래 코드에서 dorny/paths-filter Action의 역할은?
yaml

steps:
  - uses: actions/checkout@v4
  - id: filter
    uses: dorny/paths-filter@v3
    with:
      filters: .github/utils/file-filters.yaml

  - run: echo "${{ steps.filter.outputs.changes }}"
답 :

# 퀴즈 41~50번 📝

41번 아래 코드에서 id 의 역할은?
yaml

steps:
  - id: build
    run: echo "building..."
  
  - if: steps.build.outcome == 'success'
    run: echo "build succeeded!"
답 :

42번 아래 코드는 어떤 상황에서 워크플로우가 실행돼?
yaml

on:
  pull_request:
    types:
      - opened
      - synchronize
    paths:
      - "src/**"
      - "!src/**/*.test.ts"
답 :

43번 actions/checkout 은 왜 필요해?
답 :

44번 아래 코드에서 name: 과 id: 의 차이점은?
yaml

steps:
  - name: 코드 빌드하기
    id: build-step
    run: echo "building..."
답 :

45번 아래 코드의 실행 결과를 말해봐요.
yaml

env:
  WORKFLOW_VAR: hello

jobs:
  job-1:
    runs-on: ubuntu-24.04
    env:
      JOB_VAR: world
    steps:
      - env:
          STEP_VAR: "!"
        run: echo "$WORKFLOW_VAR $JOB_VAR $STEP_VAR"
      
      - run: echo "$WORKFLOW_VAR $JOB_VAR ${STEP_VAR:-<UNSET>}"
답 :

46번 GitOps 방식이 Push 방식과 다른 점은?
답 :

47번 아래 코드에서 concurrency 의 역할은?
yaml

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true
답 :

48번 task 를 사용해서 로직을 외부화하면 좋은 이유 2가지는?
답 :

49번 아래 코드에서 startsWith 의 역할은?
yaml

install_node: ${{ startsWith(matrix.service, 'services/node/') }}
답 :

50번 지금까지 배운 Action 종류 4가지를 말해봐요.
답 :