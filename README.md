# Weavework and Tetrate Webinar
(Registration [page](https://go.weave.works/webinar-security-and-resiliency-of-cloud-native-applications.html))

## Preparation steps

- Start vscode in demo machine first

- Open the following Tabs in web-browser
    - Presentation Demo [Slide](https://docs.google.com/presentation/d/1QWthI3HmddY9vmSBiav6_JnelMizwp9D9v-29uD2xFY/present?slide=id.p#19)
    - GitHub [repository](https://github.com/PetrMc/webinar)
    - Weaverworks [GitOps](https://localhost:8000/)
    > **_NOTE:_** requires forwarding in local cluster per `kubectl port-forward -n flux-system deployment/flux-system-weave-gitops-mccp-cluster-service 8000:8000`
    - TSB [Console](https://webinar-tsb.cx.tetrate.info:8443/)

- In Separate window open and keep it running
   - Application [Page](http://webinar-app.cx.tetrate.info/)

## Demo steps

### Intro steps
- Review Slide Architecture
- Walk via TSB Interface 
- Show application page
- Demo GitOps Dashbord
- Review Demo steps slide

### Adding green
- Make sure you in the main branch
    ```bash
    cd ~/GIT/webinar
    git checkout main && git fetch && git pull
    git branch -d deploying-green
    ```    
- Show the current yaml applied
- Review yamls from `green` directory
- Create new branch
    ```bash
    git checkout -b deploying-green
    ```    
- Copy yamls from green
   ```bash
   cp ~/GIT/webinar/green/* ~/GIT/webinar/apps/webinar-app/templates/
   ```
- **Bump** up helm `Chart.yaml` version 

### Discuss and demo Gitops controls
- Demo that `organization` field spelled with `s` instead of `z`
- Submit `github` changes
   ```bash
   git add . && git commit -m "Deploying Green app v2 and shifting 10% of traffic to Green" && git push --set-upstream origin deploying-green
   ```    
- Switch to Github page and see GitOps in action
- Observe the error - fix the `organization` spelling in `apps/webinar-app/lb.yaml`
- Discuss Github Actions and `policy` files
- Resubmit to Github
   ```bash
   git add . && git commit -m "Fixing yaml" && git push
   ```
- Switch back to `Github` - merge the update
- Watch in `GitOps` - the changes being applied
- Show change in `TSB` and `Web-app` panels

### Swiching more traffic to Green

- Edit `lb.yaml` in `app/webinar-app/template` to add more traffic to Green
- **Bump** up helm `Chart.yaml` version 
- Submit changes to `Github`
  ```bash
  git add . && git commit -m "Shifting more traffic to Green" && git push
  ```
- Merge the changes 
- Observe `GitOps`, `TSB` and `web-app`

### Reset

- delete all files from templates and copy `Blue` `tsb.yaml`
  ```bash
  rm apps/webinar-app/templates/*
  cp blue/*.yaml apps/webinar-app/templates/
  ```
- **Bump** up helm `Chart.yaml` version 
- Submit changes to `Github`
  ```bash
  git add . && git commit -m "Resetting to Blue" && git push
  ```
- Merge the changes 
- Confirm everything is reset to blue only
