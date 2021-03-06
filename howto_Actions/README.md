# howto_Actions โจ
<img src="https://user-images.githubusercontent.com/40287191/122417056-2ec2f380-cfc4-11eb-8147-b3e869b1fb4a.png" width="460" height="250">



# 1. ๐ฏ Actions ์์ฑ, ์ฌ์ฉ, ๊ณต์  

<details><summary> </summary>
<p>
  
  - Actions๋ ์ ์ฒด Workflow์ ๊ฐ ๋จ๊ณ๋ฅผ ๊ตฌ์ฑํ๋ ๋จ์ ์์์ด๋ฉฐ, ๊ฐ๊ฐ ์ง์ ๋ ๋์์ ์ํํฉ๋๋ค. 
  
  - ์ ์ฅ์์ ์ํธ์์ฉํ๋ action์ ์์ฑํ  ์ ์๊ณ , ์ด๊ฒ์ ์ด์ฉํด GitHub API์ ๋ค๋ฅธ third-party API์ ํตํฉํ๋ action๋ ์์ฑํ  ์ ์์ต๋๋ค. ์๋ฅผ ๋ค์ด, npm module์ publishํ๋ action, ๊ธด๊ธํ issue๊ฐ ์์ฑ๋์์ ๋ SMS alert๋ฅผ ๋ณด๋ด๋ action, ๋๋ ์์ฉํ  ์ค๋น๊ฐ๋ ์ฝ๋๋ฅผ deployํ๋ action๋ฑ์ ์์ฑํ  ์ ์์ต๋๋ค. 
  
  
  - Workflow๋ ์ฌ๋ฌ Actions๋ค์ ํฌํจํ๋ฉฐ, ๊ฐ Actions๋ค์ ์ปค๋ฎค๋ํฐ์์ ๋ง๋ค์ด์ง ๊ฒ์ ์ฌ์ฉํ๊ฑฐ๋, ์ง์  ๋ง๋ค์ด์ ์ฌ์ฉํ  ์ ์์ต๋๋ค.
    
     ```
     steps:
       - uses : {owner}/{repo}@{ref}
     ```

     ```
     steps
       - uses : ./path/to/dir 
     ```
  
  - [ํ์ฌ ์ ์ฅ์์์ ๋ง๋ค์ด์ง Actions๋ฅผ ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/finding-and-customizing-actions#referencing-an-action-in-the-same-repository-where-a-workflow-file-uses-the-action)ํ๊ธฐ ์ํด์๋ ์๋ example๊ณผ ๊ฐ์ด ๊ตฌ์ฑํฉ๋๋ค. 
  
    - ๋๋ ํ ๋ฆฌ
      ```
      |-- hello-world (repository)
      |   |__ .github
      |       โโโ workflows
      |           โโโ my-first-workflow.yml
      |       โโโ actions
      |           |__ hello-world-action
      |               โโโ action.yml
      ```
    - Workflow ํ์ผ
      ```
      jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          # This step checks out a copy of your repository.
          - uses: actions/checkout@v2
          # This step references the directory that contains the action.
          - uses: ./.github/actions/hello-world-action
      ```
  
  - ๋ง์ฝ [Docker Hub์ ์ปจํ์ด๋ ์ด๋ฏธ์ง๋ก ๋ Actions๋ฅผ ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/finding-and-customizing-actions#referencing-a-container-on-docker-hub)ํ๋ค๋ฉด ์๋์ ๊ฐ์ด ์ง์ ํฉ๋๋ค. 
  
  ```
  jobs:
   my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
  ```
  
  
  
  - ํจ๊ป ์ฌ์ฉํ  Actions๋ฅผ ์์ฑํ๋ค๋ฉด, [๋ณ๋์ ์ ์ฅ์์ Actions๋ฅผ ๋ง๋ค๊ณ  ๊ณต์ ํ๋ ๊ฒ์ด ์ข์ต๋๋ค](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/about-actions#choosing-a-location-for-your-action). (Application๋ฑ์ ์ฝ๋์ ์์ด์ง ์๊ฒ)
  
  - ํจ๊ป ์ฌ์ฉํ  Actions๋ [release management๋ฅผ ํ์ฌ version tag์ ํตํด](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/about-actions#good-practices-for-release-management) ์ฌ์ฉํ๋๋ก ํ๋ ๊ฒ์ด ์ข์ต๋๋ค. 
  
    - Tag 
    
     ```
     steps:
       - uses: actions/javascript-action@v1
     ```
  
    - Tag
     ```
     steps:
       - uses: actions/javascript-action@v1.0.1
     ```
  
    - branch
     ```
     steps:
       - uses: actions/javascript-action@v1-beta
     ```
  
    - SHA
     ```
     steps:
       - uses: actions/javascript-action@172239021f7ba04fe7327647b213799853a9eb89
     ```
 
 - [Actions์ ์ข๋ฅ](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/about-actions#types-of-actions)
   
    - Actions๋ Docker container์ JavaScript, ๊ทธ๋ฆฌ๊ณ  ์ฌ๋ฌ ๋ช๋ น์ด๋ฅผ ๋ฌถ์ด ํ๋์ action์ผ๋ก ์คํํ๋ ์ธ ๊ฐ์ง  ์์ต๋๋ค. 
    - Actions๋ ๋ฉํ๋ฐ์ดํฐ ํ์ผ์ ์ด์ฉํด input, output ๊ทธ๋ฆฌ๊ณ  main entrypoint๋ฅผ ์ง์ ํ  ์ ์์ต๋๋ค. ๋ฉํ๋ฐ์ดํฐ ํ์ผ์ ์ด๋ฆ์ `action.yml` ๋๋ `action.yaml` ์ด์ด์ผ ํฉ๋๋ค. 
    
       Type |	Operating system
       --|--
       Docker container	| Linux
       JavaScript	| Linux, macOS, Windows
       Composite run steps	| Linux, macOS, Windows
    
    - โน๏ธ ๋ฉํ๋ฐ์ดํฐ ํ์ผ(`action.yml`, `action.yaml` ) [syntax ์ฐธ์กฐ](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/metadata-syntax-for-github-actions)
       - [Syntax ์ค๋ช](actions_metadata.md)
  
  
  
 </p>
 </details>

<br/>

# 2. Actions์ ์ฃผ์ features

<details><summary> </summary>
<p>
  
  1. [Workflow๋ด Variable ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/essential-features-of-github-actions#using-variables-in-your-workflows)
    
     - GitHub Actions๋ [๊ธฐ๋ณธ ํ๊ฒฝ ๋ณ์](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environment-variables#default-environment-variables)๋ค์ ๊ฐ์ง๊ณ  ์์ต๋๋ค.
     - ๋, ํ์์ Workflow ํ์ผ๋ด์ ํ์ํ ํ๊ฒฝ ๋ณ์๋ค์ ์์ฑํ๊ณ  ์ฌ์ฉํ  ์ ์์ต๋๋ค. 
     - ์๋ ์์๋, `POSTGRES_HOST` ์ `POSTGRES_PORT`๋ฅผ ์์ฑํ๊ณ  `node client.js`์์ ์ฌ์ฉํ๋ ์์  ์๋๋ค. 
  
       ```
        jobs:
        example-job:
            steps:
              - name: Connect to PostgreSQL
                run: node client.js
                env:
                  POSTGRES_HOST: postgres
                  POSTGRES_PORT: 5432
       ```
  
     - [Environment variables](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environment-variables) ์ฐธ์กฐ
  
  <br/>
  
  2. [Workflow์ ์คํฌ๋ฆฝํธ ์ถ๊ฐ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/essential-features-of-github-actions#adding-scripts-to-your-workflow)
   
     - `run` ํค์๋๋ฅผ ์ฌ์ฉํด ์คํฌ๋ฆฝํธ๋ ์ ๋ช๋ น์ด๋ฅผ ์ํํ๋ Actions๋ฅผ ๊ตฌ์ฑํ  ์ ์์ต๋๋ค. 
  
       ```
       jobs:
         example-job:
          steps:
            - run: npm install -g bats
       ```

       ```
       jobs:
          example-job:
            steps:
              - name: Run build script
                run: ./.github/scripts/build.sh
                shell: bash
       ```
  
  <br/>
  
  3. [Job๊ฐ์ ๋ฐ์ดํฐ ๊ณต์ ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/essential-features-of-github-actions#sharing-data-between-jobs)
  
     - ๊ฐ์ workflow๋ด์์ ์ด๋ job์ด ์์ฑํ ํ์ผ์ ๋ค๋ฅธ job์ ๊ณต์ ํ๋๋ก ๊ตฌ์ฑํ  ์ ์์ต๋๋ค. 
     - ๋๋, ํฅํ์ ์ฐธ์กฐ๋ฅผ ์ํด ์์ฑ๋ ํ์ผ์ artifact๋ก ์ ์ฅํ  ์ ์์ต๋๋ค. 
     - Artifact๋ ๋น๋์ ํ์คํธ๋ฅผ ๊ฑฐ์ณ ์์ฑ๋ ํ์ผ๋ค ์๋๋ค. (์: ๋ฐ์ด๋๋ฆฌ, ํจํค์ง ํ์ผ๋ค, ํ์คํธ ๊ฒฐ๊ณผ, ๋ก๊ทธ ํ์ผ, ํ๋ฉด ์คํฌ๋ฆฐ ์ท)
     - ์๋ฅผ ๋ค์ด, ์๋์ ๊ฐ์ด ํ์ผ์ ์์ฑํ๊ณ  artifiact๋ก ์๋ก๋ ํฉ๋๋ค. 

     ```
     jobs:
        example-job:
          name: Save output
          steps:
            - shell: bash
              run: |
                expr 1 + 1 > output.log
            - name: Upload output file
              uses: actions/upload-artifact@v2
              with:
                name: output-log-file
                path: output.log
     ```

     - `actions/download-artifact` Actions๋ฅผ ์ฌ์ฉํ์ฌ, ๋ณ๋์ workflow ์คํ์์ ์์ ํ์ผ์ ๋ค์ด๋ก๋ ํ  ์ ์์ต๋๋ค. 

  
     ``` 
      jobs:
        example-job:
          steps:
            - name: Download a single artifact
              uses: actions/download-artifact@v2
              with:
                name: output-log-file
     ```
  
  <br/>
  
  4. [Secret์ ์ ์ฅ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#storing-secrets)
   
     - Workflow ๋ด์์ ํจ์ค์๋ ๋๋ certificate์ ์ฌ์ฉํด์ผ ํ  ๋, ์ ์ฅ์ ๋๋ ์กฐ์ง์ `secret`์ ์ ์ฅํ๊ณ  ํ๊ฒฝ ๋ณ์๋ก์ ์ฌ์ฉํ  ์ ์์ต๋๋ค. 
   
      ```
      jobs:
        example-job:
          runs-on: ubuntu-latest
          steps:
            - name: Retrieve secret
              env:
                super_secret: ${{ secrets.SUPERSECRET }}
              run: |
                example-command "$super_secret"
      ```
 
  <br/>
  
  5. [Dependent job ์์ฑ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#creating-dependent-jobs)
  
       - ๊ธฐ๋ณธ์ ์ผ๋ก workflow๋ด์ ๋ชจ๋  job๋ค์ ๋์์ ์คํ๋ฉ๋๋ค. ๋ฐ๋ผ์, ์ด๋ ํ job์ด ๋ฐ๋์ ๋ค๋ฅธ job์ด ๋๋ ์ดํ์ ์คํ๋์ด์ผ ํ๋ค๋ฉด, `needs` ํค์๋๋ฅผ ์ฌ์ฉํ์ฌ ์ด๋ฌํ ์์กด์ฑ์ ์ค์ ํ  ์ ์์ต๋๋ค. 

       ```
       jobs:
          setup:
            runs-on: ubuntu-latest
            steps:
              - run: ./setup_server.sh
          build:
            needs: setup
            runs-on: ubuntu-latest
            steps:
              - run: ./build_server.sh
          test:
            needs: build
            runs-on: ubuntu-latest
            steps:
              - run: ./test_server.sh
       ```
  
  <br/>
  
  6. [Build Matrix ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-a-build-matrix)
  
       - Build Matrix๋ฅผ ์ด์ฉํด OS, ํ๋ซํผ, ์ธ์ด๋ฑ์ ๋ค์ํ ์กฐํฉ์ผ๋ก ๋์์ ์ํฌ ํ๋ก์ฐ๋ฅผ ์คํํ  ์ ์์ต๋๋ค. 
       - Build Matrix๋ `strategy` ํค์๋๋ก ๊ตฌ์ฑํฉ๋๋ค. 

       ```
       jobs:
          build:
            runs-on: ubuntu-latest
            strategy:
              matrix:
                node: [6, 8, 10]
            steps:
              - uses: actions/setup-node@v2
                with:
                  node-version: ${{ matrix.node }}
       ```
   
  <br/>
  
  7. [Database์ ์๋น์ค ์ปจํ์ด๋ ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-databases-and-service-containers)
  
       - Job์ด ๋ฐ์ดํฐ๋ฒ ์ด์ค ๋๋ Cache ์๋น์ค๋ฅผ ํ์๋ก ํ๋ค๋ฉด, `services` ํค์๋๋ฅผ ์ฌ์ฉํ์ฌ ํ์์ ์ผ๋ก ์๋น์ค๋ฅผ ์์ฑํ  ์ ์์ต๋๋ค. ์ด๋ ๊ฒ ์์ฑ๋ ์ปจํ์ด๋๋ ํด๋น job๋ด ๋ชจ๋  step๋ค์ด ์ฌ์ฉํ  ์ ์๊ณ , job์ ์คํ์ด ์๋ฃ๋๋ฉด ์ญ์ ๋ฉ๋๋ค.
       - ์๋ ์๋, job์ด `services`๋ฅผ ์ฌ์ฉํด `postgre` ์ปจํ์ด๋๋ฅผ ์์ฑํ๊ณ  `node`๋ฅผ ์ฌ์ฉํด ์๋น์ค์ ์ฐ๊ฒฐํ๋ ๋ฐฉ๋ฒ์ ๋ณด์ฌ์ค๋๋ค. 

      ```
      jobs:
        container-job:
          runs-on: ubuntu-latest
          container: node:10.18-jessie
          services:
            postgres:
              image: postgres
          steps:
            - name: Check out repository code
              uses: actions/checkout@v2
            - name: Install dependencies
              run: npm ci
            - name: Connect to PostgreSQL
              run: node client.js
              env:
                POSTGRES_HOST: postgres
                POSTGRES_PORT: 5432
      ```
  
  <br/>
  
  8. [Label์ ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-labels-to-route-workflows)

       - job์ ํน์  self-hosted ๋ฌ๋์ ํ ๋นํ๊ธฐ ์ํด label์ ์ฌ์ฉํฉ๋๋ค. ํน์  ํํ์ ๋ฌ๋๊ฐ job์ ์คํํ๋๋ก ํ๊ธฐ ์ํด label์ ์ฌ์ฉํด job์ด ์คํ๋  ๋ฌ๋๋ฅผ ์ง์ ํฉ๋๋ค. 

       ```
       jobs:
        example-job:
          runs-on: [self-hosted, linux, x64, gpu]
       ```
 
  <br/>
  
  9. [Environment ์ฌ์ฉ](https://docs.github.com/en/enterprise-server@3.1/actions/learn-github-actions/managing-complex-workflows#using-environments)
  
       - Environment์ ๋ํ ๋ณดํธ ๋ฃฐ๊ณผ secret์ ์ค์ ํ  ์ ์์ต๋๋ค. 
       - ๊ฐ job์ ํ๋์ environment๋ฅผ ์ฐธ์กฐํ  ์ ์์ต๋๋ค. 
       - Job์ด ์ฐธ์กฐํ๋ environment๊ฐ ๋ฌ๋๋ก ๋ณด๋ด์ง๊ธฐ ์ ์, ํด๋น environment์ ๋ํ ๋ณดํธ๋ฃฐ์ ๋จผ์  ํต๊ณผ ํด์ผ๋ง ํฉ๋๋ค. 
       - ['Environment'](https://docs.github.com/en/enterprise-server@3.1/actions/reference/environments) ์ฐธ์กฐ
  
</p>
</details>

<br/>


# 3. Workflow ํ์ผ โพ๏ธ
 
 <details><summary> </summary>
 <p>
   
   1. โ๏ธ [Workflow ํ์ผ ๊ตฌ์กฐ](workflow_file/workflow_file_component.md)
   
   2. [Workflow ํ์ผ ํํ๋ฆฟ : ์กฐ์ง๋ด ์ํฌํ๋ก์ฐ ๊ณต์ ](workflow_file/workflow_template.md) ๐
   
   3. [Workflow ํธ๋ฆฌ๊ฑฐ](workflow_file/workflow_trigger.md) ๐ซ
   
   4. [Workflow ํ์ผ YAML ์์ ์ ์ค๋ช](workflow_file/workflow_yaml_syntax.md) ๐
   
   5. [๐ท Workflow ์คํ ๊ด๋ฆฌ](workflow_file/workflow_manage.md)
   
   6. [Workflow ๋ด์์์ ์ธ์ฆ : `GITHUB_TOKEN` ๋๋ PAT ](workflow_file/workflow_authentication.md) ๐

   7. Workflow syntax, Workflow Command, Context/Expression Syntax
     
      - โ [Workflow syntax](workflow_file/workflow_detail_syntax.md)
   
      - [Workflow Commands](workflow_file/workflow_commands.md)

      - [Context and expression syntax](workflow_file/context_and_expression_syntax.md)
   
 
 
   </p>
 </details>

<br/>
 
# 4. Docker ์ปจํ์ด๋ Actions ๐ฆ
 
 <details><summary> </summary>
 <p>
   
   - Docker ์ปจํ์ด๋๋ GitHub Actions์ ์ฝ๋์ ์คํํ๊ฒฝ์ ํจ๊ป ํจํค์งํฉ๋๋ค. ์ด๊ฒ์ Actions์ ์ฌ์ฉ์๊ฐ tool์ด๋ ์์กด์ฑ๋ฑ์ ๊ฑฑ์ ํ  ํ์์์ด ๋์ฑ ์ผ๊ด๋๊ณ  ์ ๋ขฐํ  ์ ์๋ action ์คํ ๋จ์๋ฅผ ๋ง๋ค์ด ์ค๋๋ค. 
   - Docker ์ปจํ์ด๋๋ฅผ ํตํด OS์ ํน์  ๋ฒ์ ผ, ์์กด์ฑ, tools์ ์ฝ๋๋ฅผ ์ฌ์ฉํ  ์ ์์ต๋๋ค. ํน์ ํ ํ๊ฒฝ ๊ตฌ์ฑ์์ ๋์ํด์ผ๋ง ํ๋ actions๋ค์ Docker๊ฐ ๊ฐ์ฅ ์ ํฉํ ๋ฐฉ๋ฒ์๋๋ค. ์ปจํ์ดํฐ๋ฅผ ์์ฑํ๊ณ  ํ์ํ ๊ฒ๋ค์ ๊ฐ์ ธ์ค๋ ๋ฐ ์์๋๋ latency๋ก ์ธํด JavaScript actions์ ๋นํด ๋๋ฆฝ๋๋ค.
   - Docker ์ปจํ์ด๋ actions๋ Linux์ ๋ฌ๋์์๋ง ์คํ๋ฉ๋๋ค. Self-hosted ๋ฌ๋๋ OS๋ก Linux, ๊ทธ๋ฆฌ๊ณ  Docker๊ฐ ํจ๊ป ์ค์น๋์ด ์์ด์ผ Docker ์ปจํ์ด๋ action์ ์คํํ  ์ ์์ต๋๋ค. 
   
   - [Docker ์ปจํ์ด๋ actions ์์ฑ ๋ฐฉ๋ฒ ์์](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/creating-a-docker-container-action)
   
 </p>
 </details>
 
<br/>
 

# 5. JavaScript Actions ๐

 <details><summary> </summary>
 <p>
   
   - JavaScript actions๋ ๋ฌ๋ ๋จธ์ ์์ ์ง์ ์ ์ผ๋ก ์คํ๋๊ณ , action์ ์ฝ๋๊ฐ ์ฝ๋๋ฅผ ์คํํ๋๋ฐ ์ฌ์ฉ๋๋ ํ๊ฒฝ์ผ๋ก ๋ถํฐ ๋ถ๋ฆฌ๋ฉ๋๋ค. 

   - JavaScript actions๋ฅผ ์ด์ฉํ๋ฉด Docker ์ปจํ์ด๋ action๋ณด๋ค action์ ์ฝ๋๋ฅผ ๋ ๋จ์ํํ๊ณ , ๋ ๋น ๋ฅด๊ฒ ์คํํ  ์ ์์ต๋๋ค. 
   
   - JavaScript actions๊ฐ ๋ชจ๋  GitHub-hosted runners (Ubuntu, Windows, macOS)์ ํธํ๋  ์ ์๋๋ก ํ๊ธฐ ์ํด, ์ฌ๋ฌ๋ถ์ด ์์ฑํ๋ JavaScript ์ฝ๋๋ ์จ์ ํ JavaScript์ฌ์ผ ํ๊ณ , ๋ค๋ฅธ ๋ฐ์ด๋๋ฆฌ๋ค์ ์์กดํ๋ฉด ์๋ฉ๋๋ค. JavaScript actions๋ ๋ฌ๋์์ ์ง์ ์ ์ผ๋ก ์คํ๋๋ฉฐ, virtual environment์ ์ด๋ฏธ ์กด์ฌํ๋ ๋ฐ์ด๋๋ฆฌ๋ค์ ์ฌ์ฉํฉ๋๋ค.
   
   - ์ฌ๋ฌ๋ถ์ด Node.js ํ๋ก์ ํธ๋ฅผ ๊ฐ๋ฐํ๋ค๋ฉด, ์ฌ๋ฌ๋ถ์ด ์ฌ์ฉํ  ์ ์๋ GitHub Actions Toolkit์ ์ฌ์ฉํ์ฌ ๋ ๋น ๋ฅด๊ฒ ๊ฐ๋ฐํ  ์ ์์ต๋๋ค. (์ถ๊ฐ์ ๋ณด๋ actions/toolkit repository์ฐธ์กฐ)
   
   - [JavaScript actions ์์ฑ ๋ฐฉ๋ฒ ์์](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/creating-a-javascript-action)
   
   
   
 </p>
 </details>
 
 <br/>
 

# 6. Composite run steps Actions

 <details><summary> </summary>
 <p>

   - _Composite run steps_ actions๋ ํ๋์ action์ ์ฌ๋ฌ๊ฐ์ steps๋ค์ ๋ฌถ์ด ์คํ์ํฌ ์ ์์ต๋๋ค.
   
   - ์๋ฅผ ๋ค์ด, ์ฌ๋ฌ๊ฐ์ run ๋ช๋ น์ด๋ฅผ ํ๋์ action์ ๋ฌถ์ด์ ์ํฌํ๋ก์ฐ๊ฐ ์ด ๋ฌถ์ ๋ช๋ น์ด๋ฅผ ํ๋์ step์ผ๋ก ์ฒ๋ฆฌํ๋๋ก ํ๋ ๋ฐฉ์์๋๋ค. 
   
   - [Composite run step action ์์ฑ ๋ฐฉ๋ฒ ์์](https://docs.github.com/en/enterprise-server@3.1/actions/creating-actions/creating-a-composite-run-steps-action)
 
 </p>
 </details>

 <br/>
 



