# Weavework and Tetrate Wwebinar

## Preparation steps

- Start vscode in demo machine first

- Open the following Tabs in web-browser
    - Presentation Demo [Slide](https://docs.google.com/presentation/d/1QWthI3HmddY9vmSBiav6_JnelMizwp9D9v-29uD2xFY/present?slide=id.p#27)
    - Registration [page](https://go.weave.works/webinar-security-and-resiliency-of-cloud-native-applications.html)
    - GitHub [repository](https://github.com/PetrMc/webinar)
    - Weaverworks [GitOps](https://localhost:8000/)
    > **_NOTE:_** requires forwarding in local cluster per `kubectl port-forward -n flux-system deployment/flux-system-weave-gitops-mccp-cluster-service 8000:8000`

- In Separate window open and keep it running
   - Application - http://webinar-app.cx.tetrate.info/

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
    git branch -d deploying-green
    git checkout main && git fetch && git pull
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
- Bump up helm `Chart.yaml` version 

### Discuss and demo Gitops controls
- Misspell `organization` field
- Submit `github` changes
   ```bash
   git add . && git commit -m "Deploying Green app v2 and shifting 10% of traffic to Green" && git push --set-upstream origin deploying-green
   ```    
- Switch to Github page and see GitOps in action
- Observe the error - fix the `organization` spelling
- Resubmit to Github
   ```bash
   git add . && git commit -m "Fixing yaml" && git push
   ```
- Switch back to `Github` - merge the update
- Watch in `GitOps` - the changes being applied
- Show change in `TSB` and `Web-app` panels

### Swiching more traffic to Green

- Edit `tsb.yaml` in `app/webinar-app/template`
- Bump up helm `Chart.yaml` version 
- Submit changes to `Github`
   ```bash
   git add . && git commit -m "Shifting more traffic to Green" && git push
   ```
- Merge the changes 
- Observe `GitOps`, `TSB` and `web-app`




