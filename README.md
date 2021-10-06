

# Robust Tjänst by Netnod

Robust Tjänst is a test tool for web sites with the intention of making the internet a better place.

## What it is / what it will be

We aim to establish a minimum level of requirements, a de facto standard, for all websites to be considered reliable. We encourage everyone to be involved in this process and we have just started building the basic building blocks.

These are some examples of what we aim to create: 

    docker run -rm netnod/robust-dns https://www.example.com
    docker run -rm netnod/robust-tls https://www.example.com
    docker run -rm netnod/robust-ipv6 https://www.example.com

and maybe combine them to one test:

    docker run -rm netnod/robust-tjanst https://www.netnod.se

To make it easier to use we are also planning to create a live badge for you to use when you have reached the minimum level. This badge will be keeping track on changes to your site so you and your visitors can be sure that when things change- either in the requirements, updates in standards or you move your domain or switch hosting provider that everything is still OK.

## Current status

We are just getting started. These are some milestones that we think will be important. 

- [x] Basic site 
- [x] Scheduling tests running safely in Kubernetes
- [x] Name of the project: Robust Tjänst
- [x] Template for test runners
- [ ] Build an open source community <- we/you are here ❤️
- [ ] Logotype and badge design
- [ ] Implement basic tests for minimum requirements
- [ ] Register and run tests in background
- [ ] Launch 🎉
- [ ] Continue developing as open source
- [ ] Spread the word

# How to contribute

At this point we are looking for general feedback of the idea, input on minimum level of tests/requirements. If you want to contribute to the code, please bare with us - the codebase is still very young. With that said, what we really would love at this point is to get your help to produce tests. Look at the [example tests](packages/tests) to get started.

If you find any bugs or have ideas we are super happy for [issues](issues) or even [pull requests](pulls).

Note: All code is released under the [BSD 3-Clause License](LICENSE).
   
### What is a minimum level?

A good minimum level is what is an acceptable level of security. Passing should be easy, and failing should be bad.

When the minimum level for a site isn't reached we want it to be very easy to understand:

  1. Why it is bad in words that can be understood by those who are not experts.
  2. What to do to fix it
  3. Why it is a good idea to invest in fixing the problems
  4. A carrot when they are fixed (the ❤️ badge)

### Help people be better
We want to help people reach the minimum acceptable level by giving clear instructions.

# Setup solution

To set up the whole solution you will need a Kubernetes cluster, either a local one (Minikube, MicroK8s or Docker Desktop) or a cloud environment such as GKE, EKS, AKS.

To deploy the solution you will need Skaffold and make sure you are in the right Kubernetes context and run:

    skaffold run

## Build and test a robust test:

    cd packages/tests/[test name]
    docker build -t [test name] .
    docker run -rm [test name]

You can create your own test by adapting some of our examples. Each test should return a zero if succeeded and a non-zero if failed. Also it should emit a json explaining the steps that failed and a short description on how to mitigate the errors. The format of the returned JSON is not decided yet. We aim to find a standard here on a parsable format which is both readable in a command line and can be used to help users in the website.

## Development of the website

```
nvm use
npm install -g yarn
yarn
```

### Database
```
# inside packages/web/ 

createuser robust
createdb robust-tjanst -O robust
psql -d robust-tjanst -U robust < packages/service/src/db/schema.sql

# seed is optional
DATABASE_URL=postgres://robust@localhost/robust-tjanst yarn run db:seed
```

# Run
## Locally
```
cd packages/web && yarn run:dev # reloads on file changes
```

## LICENSE

(c) Copyright 2021 Netnod AB - All code is released under the [BSD 3-Clause License](LICENSE).
