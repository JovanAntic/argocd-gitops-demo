# argocd-gitops-demo
ArgoCD GitOps Demo - Linux DevOps Projekat
Demo projekat koji ilustruje **GitOps** princip kontinuiranog deploymenta na Kubernetes klaster koristeći **Argo CD**.

## Šta projekat pokazuje

Ideja GitOps-a je da Git repozitorijum bude **jedini izvor istine** (source of truth) za željeno stanje klastera — umesto ručnog `kubectl apply`, Argo CD kontinuirano prati ovaj repo i automatski sinhronizuje stanje klastera sa onim što je definisano ovde. Ako neko ručno izmeni resurs u klasteru, Argo CD to prijavljuje kao "OutOfSync" i može automatski da vrati stanje u sklad sa Git-om.

## Struktura repozitorijuma

- **`argocd-apps/`** — Argo CD `Application` manifesti koji definišu koje aplikacije Argo CD treba da prati i deployuje
- **`environments/`** — razdvajanje konfiguracije po okruženjima (npr. dev/prod/staging), u skladu sa GitOps praksom da svako okruženje ima svoju granu ili folder
- **`guestbook/`** — primer jednostavne aplikacije (standardni Argo CD tutorial primer) korišćen za demonstraciju sync procesa
- **`nginx-app/`** — Kubernetes manifesti za Nginx deployment, korišćeni kao drugi test primer
- **`tutorial/`** — beleške/koraci koje sam pratio dok sam savladavao Argo CD
- **`argocd-nginx-app.yaml`** — Argo CD Application manifest koji povezuje ovaj repo sa Nginx deploymentom u klasteru

## Kako radi (ukratko)

1. Argo CD se instalira u Kubernetes klaster (namespace `argocd`)
2. Registruje se ovaj Git repo kao izvor za `Application` resurs (npr. `argocd-nginx-app.yaml`)
3. Argo CD kontinuirano upoređuje stanje definisano u repou sa stvarnim stanjem u klasteru
4. Promena u ovom repou (git push) automatski (ili uz ručni sync) menja stanje deploymenta u klasteru

## Lieratura
[1] B. Yuen, A. Matyushentsev, T. Ekenstam, J. Suen, GitOps and Kubernetes: Continuous Deployment with Argo CD, Jenkins X, and Flux, Manning Publications, Shelter Island, 2021.
[2] OpenGitOps (CNCF), GitOps Principles v1.0.0, https://opengitops.dev/ 
[3] The Argo Project, Argo CD – Declarative GitOps CD for Kubernetes, https://argo-cd.readthedocs.io/.
[4] A. Richardson, GitOps – Operations by Pull Request, Weaveworks blog, 2017, https://www.weave.works/blog/gitops-operations-by-pull-request
[5] The Kubernetes Authors, Kubernetes Documentation, https://kubernetes.io/docs/home/ (pristupljeno 12.10.2026).
[6] Kustomize, Kustomize – Kubernetes native configuration management, https://kustomize.io/ (pristupljeno 12.10.2026).
[7] The Helm Authors, Helm Documentation, https://helm.sh/docs/
[8] rslim087a, ArgoCD Kubernetes GitOps Tutorial, GitHub repozitorijum, https://github.com/rslim087a/argocd-kubernetes-gitops-tutorial
[9] K. Kapelonis, Stop Using Branches for Deploying to Different GitOps Environments, Codefresh, 2021, https://codefresh.io/blog/stop-using-branches-deploying-different-gitops-environments/ (pristupljeno 04.11.2026)


## Šta sam ovim vežbao

- Deklarativni pristup deploymentu (Infrastructure as Code / GitOps)
- Razdvajanje konfiguracije po okruženjima
- Osnovni rad sa Kubernetes manifestima (Deployment, Service)
- Rad sa Argo CD `Application` CRD-om
