# Humanitec Score + Backstage TraderX Demo

This repository demonstrates a full Internal Developer Platform and Golden Path (IDP) setup for the **TraderX** microservices demo using:

- [Score](https://score.dev/) to define portable workloads  
- [Humanitec Resource Definitions](https://docs.humanitec.com/integrations/resource-definitions/) for dynamic infra provisioning  
- [Backstage](https://backstage.io/) for developer self-service  
- [PocketIDP](https://github.com/Humanitec-Dev/PocketIDP) to run the IDP locally with zero cost  

Built from a **Platform Engineer's perspective**, this project enables teams to scaffold services, manage infrastructure, and deploy workloads via **self-service Golden Paths**.

---

## 🧰 Prerequisites

Before using this project, ensure you have the following:

| Tool                         | Description                                                  |
|------------------------------|--------------------------------------------------------------|
| ✅ [PocketIDP]               | Run Backstage, GitOps, and Humanitec Agent locally           |
| ✅ Humanitec Account         | Needed to register your app, org, and definitions            |
| ✅ `score` CLI               | To build and validate Score specs                            |
| ✅ `score-k8s` / `score-compose` | Deploy locally without Humanitec                           |
| ✅ `humctl` CLI              | To interact with Humanitec APIs from your terminal           |

---

## 👷 Platform Engineer Workflow

Platform Engineers are responsible for defining and wiring the platform foundations so developers can deploy with minimal friction.

### Step-by-step:

1. **Apply Resource Definitions**

   Located in [`humanitec-resource-definitions/`](-humanitec-resource-definitions/), these map abstract resources requests in `score.yaml` to real infrastructure like Postgres, Redis, or DNS.

   ```bash
   humctl create -f humanitec-resource-definitions/


2. **Register Backstage Templates**

   * Use `catalog-info.yaml` to register templates with Backstage.
   * Templates can be added from the backendin the backstage app-config directory.
   * Templates can be imported via Backstage UI or synced via Git (e.g., Gitea for pocketIDP).


3. **Enable Golden Path Templates**

   Developers will now see TraderX service templates in the Backstage portal for self-service provisioning.

---

## 👨‍💻 Developer Workflow

Once the platform is set up:

1. **Access Backstage**

   Launch Backstage locally via PocketIDP (usually at [http://localhost:7007](http://localhost:7007)).

2. **Create a New App**

   Use TraderX template to scaffold a microservice.

3. **Customize Inputs**

   Define name. 
   
   (Using the humanitec pipleine, this deploys and creates the Humanitec application and environment automatically).

4. **Pushes to Git**

   Score-based workload structure is generated and committed to Git automatically.

5. **Humanitec Deployment**

   Humanitec picks up the Score workload and provisions infrastructure + deployment using the registered resource definitions.

---

## ⚙️ Local Deployment with Score Drivers

> 🧱 This demo builds upon the official [**TraderX CLI Tutorial**](https://github.com/Humanitec-DemoOrg/traderx-demo), part of the [Humanitec-DemoOrg](https://github.com/Humanitec-DemoOrg) collection — which showcases how to deploy Score workloads using CLI tools like `score-compose`, `score-k8s`, and `humctl`.


To run services locally using the same Score spec and Humanitec drivers:

```bash
# Validate the Score workload
score validate -f score.yaml

# Run with Docker Compose
score-compose run -f score.yaml

# Run on local Kubernetes (e.g., kind, minikube)
score-k8s run -f score.yaml

# Deploy to Humanitec environment
humctl deploy \
  --app online-boutique \
  --env development \
  -f score.yaml \
  --message "Deploying Online Boutique via CLI"
```

The **official demo focuses on CLI-based deployment and dynamic infra provisioning**.

This repo extends that foundation by:

✅ Turning workloads into reusable **Backstage Golden Paths**
✅ Wiring the experience into a **self-service IDP portal**
✅ Running everything locally using **PocketIDP** for rapid iteration
✅ Giving developers a visual interface to scaffold, deploy, and manage services

> 🔁 You get the best of both worlds: the CLI power of the official tutorial and the seamless self-service UX of Backstage + Humanitec.

---

## 📁 Project Structure

```
.
├── humanitec-backstage/content/src/score.deploy.yaml                         # Main Score workload spec
├── humanitec-resource-definitions/   # Infrastructure mapping files
├── humanitec-backstage/template.yaml              # Backstage software templates
├── .github/workflows/deploy.yaml         # GitHub Actions CI config
└── README.md                         # This file
```

---

## 📘 Reference Tutorial Repo

To understand the full context and guided setup of TraderX with Humanitec:

📦 [Humanitec-DemoOrg/traderx-demo](https://github.com/Humanitec-DemoOrg/traderx-demo)

> It includes advanced scenarios, CI/CD integrations, and local env support.

---

## 🧠 Why This Matters

This demo shows how Platform Engineers can:

* Abstract infra behind clear interfaces using Humanitec
* Enable developers to provision services via Backstage
* Use Score to ensure portability across environments
* Reduce cognitive load with pre-wired infrastructure

All powered by **PocketIDP**, **Backstage**, and **Humanitec’s Workload Platform**.

---

## 🛡 Maintainers

This project is maintained by Platform Architects committed to simplifying infrastructure and empowering developers through platform-as-a-product tooling.

---

## 📚 Resources

* [Score.dev](https://score.dev)
* [Humanitec Docs](https://developers.humanitec.com)
* [Backstage](https://backstage.io)
* [PocketIDP](https://github.com/InternalDeveloperPlatform/PocketIDP)
* [Platform Engineering Slack](https://platformengineering.org/slack)

```
