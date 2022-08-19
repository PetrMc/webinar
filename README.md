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
- Show the current yaml applied
- Review yamls from `green` directory
- Copy yamls from green
   ```bash
   ~/GIT/webinar/blue/
   ```
- Bump up helm `Chart.yaml` version 

### Discuss and demo Gitops controls
- Misspell `organization` field
- Submit `github` changes
   ```bash
   


