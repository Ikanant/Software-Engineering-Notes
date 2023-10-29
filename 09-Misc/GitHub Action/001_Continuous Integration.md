Continuous Integration

Saturday, February 11, 2023

11:32 PM

 

<https://github-actions-hero.vercel.app/>

 

Part of the reason GitHub Action is so great is because a lot of the work has already been done by the community. From actions shared for specific type of application workflows, to even tools like GitHub Actions Hero which visually shows you what your workflow is doing in order to familiarize yourself even further with the technology.

 

I started playing around in a brand new repo I will call github-actions-playuground where I will be making changes and experimenting with the Actions tools... I will only note down **new** things not mentioned in notes before... for example:\
 

![18 strategy: matrix: ](001_Continuous_Integration_000.png)

 

A strategy creates a build matrix for our jobs... We can define different variations of an environment to run each job. So in the screenshot above we are just creating a matrix.node-version variable:

 

![21 22 23 24 25 steps: - uses: - name: uses: with: actions/checkout@v2 use Node. js \${{ matrix.no actions/setup-node@vl ](001_Continuous_Integration_001.png)

 

That will spin three different instances of the build job:

![Some checks were not successful 1 failing and 2 cancelled checks O Node.js CI I build (14.x) (pull_request) Failing after 33s x (D O Node.js Cl I build (16.x) (pull_request) Cancelled after 39s o O Node.js CI I build (18.x) (pull_request) Cancelled after 39s This branch has no conflicts with the base branch Merging can be performed automatically. ](001_Continuous_Integration_002.png)

 

One thing to note is that jobs will be cancelled if one of them fails... I am guessing this can be tweaked.

 

The failure here is set because:\
 

![f- Node.js Cl O Create Cl github action for Node #1 G) Summary Jobs I O build (14.x) O build (16.x) O build (18.x) Run details Usage Workflow file build (14.x) failed 5 minutes ago in 33s Set up job Run actions/checkout@v3 I 4 5 6 7 8 9 10 11 12 13 14 use Node.js 14.x Run npm ci Run npm run build \--if-present Run npm test Run npm test \> test \> npx standard npx jest npx: installed 282 in 14.706s No tests found, exiting with code 1 Run with \'---passWithNoTests\' to exit with code In /home/ 7 files checked. testHatch: \[tjls• testPathIgnorePatterns: /node_modutes/ --- 7 matches ](001_Continuous_Integration_003.png)

 

 

**CUSTOMIZE A WORFKLOW BEYOND A TEMPLATE**

 

-   Test against multiple target environments

    -   So we know our supported OS and Node versions are working

-   Dedicated test jobs

    -   We can separate out build/test details

-   Access to artifacts

    -   So we can deploy to target env

-   Branch Protection

    -   So master can\'t be deleted or broken

-   Required reviews

    -   All PR(s) need to be doubled checked by team mates

-   Obvious Approvals

    -   So we can operate quickly and potentially automate merges and deployments

 

 

JOBS RUN IN PARALLEL !!!

![11 12 13 14 15 16 17 18 19 2ø 21 22 23 24 25 26 27 28 29 3ø 31 32 33 34 35 36 37 38 39 jobs: build: runs---on: ubuntu---tatest steps: - uses: actions/checkout@v3 - run: I npm ci npm run build \--if---present - uses: actions/upload---artifactea! With: name: build artifact path: public/ test: runs---on: ubuntu---tatest strategy: matrix: os: \[ubuntu---tatest, windows-2Ø19: node-version: \[14.x, 16.xl steps: - uses: with: name: build artifact path: public/ - uses: actions/checkout@v3 - name: Use Node. js matrix. nodt uses: actions/setup---node@v3 with: ](001_Continuous_Integration_004.png)

(Ignore the download artifact error in the test step)... but here we know that things are not going to work either way since tests is going to run at the same time as build

 

![23 24 25 26 27 path: public/ test: runs---on: ubuntu---latest needs: build ](001_Continuous_Integration_005.png)

 

**Needs:** will get us sorted out here

 

 

At the end everything works like:\
 

![](001_Continuous_Integration_006.png)

 

 

 

![Actions We Have Used actions/checkout@v2 actions/upload-artifact actions/download-artifact actions/setup-node@vl ](001_Continuous_Integration_007.png)

 

Let\'s have one last fun one to generate GIFs in our PR(s)\
 

![1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 name: GIPHY generator on: issues: types: \[opened, pull_request : types: \[opened, issue comment: edited) edited) types: \[created, edited) jobs: giphy-generator: runs-on: ubuntu-latest steps : - name: uses: env: GIPHY Generator IAmHughes/giphy-generatc ](001_Continuous_Integration_008.png)

 
