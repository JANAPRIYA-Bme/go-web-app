# Go Web Application

This is a simple website written in Golang. It uses the `net/http` package to serve HTTP requests.

## Running the server

To run the server, execute the following command:

```bash
go run main.go
```

The server will start on port 8080. You can access it by navigating to `http://localhost:8080/courses` in your web browser.

## Looks like this

![Website](static/images/golang-website.png)



<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Go Web App: End-to-End DevOps on AWS EKS</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500&family=IBM+Plex+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #f7f9fb;
    --surface: #ffffff;
    --ink: #17212b;
    --muted: #55626f;
    --line: #d9e0e7;
    --accent: #0a6c8f;
    --accent-soft: #e2f1f6;
    --code-bg: #14202b;
    --code-ink: #dbe7f0;
    --fill-bg: #fff3c4;
    --fill-ink: #5c4600;
    --box: #ffffff;
    --box-line: #9fb2c2;
  }
  @media (prefers-color-scheme: dark) {
    :root {
      --bg: #10161c;
      --surface: #17202a;
      --ink: #e6edf3;
      --muted: #9aa8b5;
      --line: #2a3643;
      --accent: #5cc0e0;
      --accent-soft: #16313c;
      --code-bg: #0a1015;
      --code-ink: #dbe7f0;
      --fill-bg: #4a3d0f;
      --fill-ink: #ffe9a0;
      --box: #1d2833;
      --box-line: #4a5d6e;
    }
  }
  * { box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    margin: 0;
    background: var(--bg);
    color: var(--ink);
    font-family: "IBM Plex Sans", system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
    line-height: 1.65;
    font-size: 16px;
  }
  .page { max-width: 880px; margin: 0 auto; padding: 48px 24px 80px; }
  h1 { font-size: 2.1rem; line-height: 1.2; margin: 0 0 12px; font-weight: 600; }
  h2 {
    font-size: 1.35rem; margin: 52px 0 14px; padding-bottom: 8px;
    border-bottom: 1px solid var(--line); font-weight: 600;
  }
  h3 { font-size: 1.05rem; margin: 28px 0 8px; font-weight: 600; }
  p { margin: 0 0 14px; max-width: 72ch; }
  a { color: var(--accent); }
  .lede { font-size: 1.1rem; color: var(--muted); max-width: 66ch; }
  .note {
    background: var(--accent-soft); border-left: 4px solid var(--accent);
    padding: 12px 16px; border-radius: 4px; margin: 20px 0; max-width: 72ch;
  }
  .fill {
    background: var(--fill-bg); color: var(--fill-ink);
    padding: 1px 6px; border-radius: 3px; font-size: .92em;
  }
  table { width: 100%; border-collapse: collapse; background: var(--surface); border: 1px solid var(--line); border-radius: 6px; overflow: hidden; }
  th, td { text-align: left; padding: 10px 14px; border-bottom: 1px solid var(--line); vertical-align: top; }
  th { background: var(--accent-soft); font-weight: 600; font-size: .95rem; }
  tr:last-child td { border-bottom: none; }
  td:first-child { white-space: nowrap; font-weight: 500; }
  .table-wrap { overflow-x: auto; }
  pre {
    background: var(--code-bg); color: var(--code-ink);
    padding: 16px 18px; border-radius: 6px; overflow-x: auto;
    font-family: "IBM Plex Mono", ui-monospace, Menlo, Consolas, monospace;
    font-size: .88rem; line-height: 1.55; margin: 10px 0 18px;
  }
  code { font-family: "IBM Plex Mono", ui-monospace, Menlo, Consolas, monospace; font-size: .9em; }
  p code, li code, td code {
    background: var(--accent-soft); padding: 1px 6px; border-radius: 3px;
  }
  ol, ul { padding-left: 22px; max-width: 72ch; }
  li { margin-bottom: 6px; }
  .diagram {
    background: var(--surface); border: 1px solid var(--line); border-radius: 6px;
    padding: 12px; overflow-x: auto;
  }
  .diagram svg { min-width: 760px; width: 100%; height: auto; display: block; }
  .box { fill: var(--box); stroke: var(--box-line); stroke-width: 1.5; }
  .box.key { stroke: var(--accent); stroke-width: 2; }
  .lbl { fill: var(--ink); font: 500 14px "IBM Plex Sans", system-ui, sans-serif; text-anchor: middle; }
  .small { fill: var(--muted); font: 400 12px "IBM Plex Sans", system-ui, sans-serif; text-anchor: middle; }
  .arrow { stroke: var(--muted); stroke-width: 1.6; fill: none; }
  .lane { fill: var(--muted); font: 600 12px "IBM Plex Sans", system-ui, sans-serif; }
  .shots { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 14px; }
  .shot {
    border: 1px dashed var(--box-line); border-radius: 6px; padding: 28px 14px;
    text-align: center; color: var(--muted); background: var(--surface); font-size: .95rem;
  }
  footer { margin-top: 56px; padding-top: 18px; border-top: 1px solid var(--line); color: var(--muted); font-size: .95rem; }
  :focus-visible { outline: 3px solid var(--accent); outline-offset: 2px; }
  @media (max-width: 600px) {
    h1 { font-size: 1.7rem; }
    .page { padding: 32px 16px 60px; }
  }
</style>
</head>
<body>
<main class="page">

  <h1>Go Web App: End-to-End DevOps on AWS EKS</h1>
  <p class="lede">A DevOps project that takes a Go web application from source code to a running deployment on Amazon EKS, using Docker, Kubernetes, Helm, GitHub Actions for CI, and Argo CD for GitOps-based delivery.</p>

  <div class="note">
    This repository is a fork of <a href="https://github.com/iam-veeramalla/go-web-app">iam-veeramalla/go-web-app</a>. The application code (<code>main.go</code>, <code>static/</code>, tests) is the original sample app. The DevOps work listed under <a href="#built">What I built</a> is mine.
  </div>
  <p>Demo video: <span class="fill">paste your demo video link here</span></p>

  <h2 id="architecture">Architecture</h2>
  <div class="diagram">
    <svg viewBox="0 0 900 340" role="img" aria-label="Architecture: developer pushes to GitHub, GitHub Actions builds and pushes an image and updates the tag, Argo CD syncs to EKS, users reach the app through Route 53 and a load balancer, Prometheus and Grafana monitor the cluster.">
      <defs>
        <marker id="head" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse">
          <path d="M0 0 L10 5 L0 10 z" fill="var(--muted)"/>
        </marker>
      </defs>

      <text class="lane" x="20" y="22">Delivery</text>
      <rect class="box" x="20"  y="50" width="140" height="46" rx="6"/><text class="lbl" x="90"  y="78">Developer</text>
      <rect class="box" x="200" y="50" width="140" height="46" rx="6"/><text class="lbl" x="270" y="78">GitHub repo</text>
      <rect class="box key" x="380" y="50" width="140" height="46" rx="6"/><text class="lbl" x="450" y="78">GitHub Actions</text>
      <rect class="box" x="560" y="50" width="140" height="46" rx="6"/><text class="lbl" x="630" y="78">Docker Hub</text>
      <path class="arrow" d="M160 73 H198" marker-end="url(#head)"/>
      <path class="arrow" d="M340 73 H378" marker-end="url(#head)"/>
      <path class="arrow" d="M520 73 H558" marker-end="url(#head)"/>
      <path class="arrow" d="M450 50 C450 20 270 20 270 48" marker-end="url(#head)"/>
      <text class="small" x="360" y="26">update image tag</text>

      <text class="lane" x="20" y="140">Cluster</text>
      <rect class="box key" x="200" y="160" width="140" height="46" rx="6"/><text class="lbl" x="270" y="188">Argo CD</text>
      <rect class="box key" x="380" y="160" width="140" height="46" rx="6"/><text class="lbl" x="450" y="188">Amazon EKS</text>
      <rect class="box" x="560" y="160" width="140" height="46" rx="6"/><text class="lbl" x="630" y="188">Prometheus</text>
      <rect class="box" x="740" y="160" width="140" height="46" rx="6"/><text class="lbl" x="810" y="188">Grafana</text>
      <path class="arrow" d="M270 160 V98" marker-end="url(#head)"/>
      <text class="small" x="300" y="134">watches</text>
      <path class="arrow" d="M340 183 H378" marker-end="url(#head)"/>
      <path class="arrow" d="M520 183 H558" marker-end="url(#head)"/>
      <path class="arrow" d="M700 183 H738" marker-end="url(#head)"/>

      <text class="lane" x="20" y="252">Traffic</text>
      <rect class="box" x="20"  y="272" width="140" height="46" rx="6"/><text class="lbl" x="90"  y="300">User</text>
      <rect class="box" x="200" y="272" width="140" height="46" rx="6"/><text class="lbl" x="270" y="300">Route 53</text>
      <rect class="box" x="380" y="272" width="140" height="46" rx="6"/><text class="lbl" x="450" y="300">Load balancer</text>
      <path class="arrow" d="M160 295 H198" marker-end="url(#head)"/>
      <path class="arrow" d="M340 295 H378" marker-end="url(#head)"/>
      <path class="arrow" d="M450 272 V208" marker-end="url(#head)"/>
    </svg>
  </div>
  <p style="margin-top:10px;color:var(--muted);font-size:.92rem;">If you have your own architecture image, add it to the repo as <code>images/architecture.png</code> and show it in the README with <code>![Architecture](images/architecture.png)</code>.</p>

  <h2 id="built">What I built</h2>
  <div class="table-wrap">
  <table>
    <tr><th>Component</th><th>Details</th></tr>
    <tr><td>Dockerfile</td><td>Containerizes the Go application</td></tr>
    <tr><td>Kubernetes manifests</td><td>Deployment, Service, and Ingress in <code>k8s/manifest/</code></td></tr>
    <tr><td>Helm chart</td><td>Templated deployment in <code>helm/go-web-app-chart/</code></td></tr>
    <tr><td>CI pipeline</td><td>GitHub Actions workflow in <code>.github/workflows/</code> that builds and pushes the image, then updates the image tag in the Helm values</td></tr>
    <tr><td>GitOps CD</td><td>Argo CD watches this repo and syncs changes to the EKS cluster automatically</td></tr>
    <tr><td>Networking</td><td>Ingress with an AWS load balancer and a Route 53 DNS record</td></tr>
    <tr><td>Monitoring</td><td>Prometheus and Grafana for cluster and application metrics</td></tr>
  </table>
  </div>

  <h3>What was provided</h3>
  <p>The Go web application source (<code>main.go</code>, <code>main_test.go</code>, <code>go.mod</code>, <code>static/</code>) from the original repository.</p>

  <h2 id="stack">Tech stack</h2>
  <div class="table-wrap">
  <table>
    <tr><th>Area</th><th>Tools</th></tr>
    <tr><td>Application</td><td>Go</td></tr>
    <tr><td>Containerization</td><td>Docker</td></tr>
    <tr><td>Orchestration</td><td>Kubernetes (Amazon EKS), Helm</td></tr>
    <tr><td>CI</td><td>GitHub Actions</td></tr>
    <tr><td>CD / GitOps</td><td>Argo CD</td></tr>
    <tr><td>Networking</td><td>Ingress, AWS load balancer, Route 53</td></tr>
    <tr><td>Monitoring</td><td>Prometheus, Grafana</td></tr>
    <tr><td>Cloud</td><td>AWS (EKS, EC2, VPC, IAM, EBS, Route 53)</td></tr>
  </table>
  </div>

  <h2 id="structure">Repository structure</h2>
<pre>.
├── .github/workflows/     # GitHub Actions CI pipeline
├── helm/
│   └── go-web-app-chart/  # Helm chart (templates and values)
├── k8s/
│   └── manifest/          # Kubernetes manifests
├── static/                # Web pages served by the app
├── Dockerfile             # Container image build
├── main.go                # Go application
├── main_test.go           # Application tests
├── go.mod
├── images/                # Architecture diagram and screenshots
└── README.md</pre>

  <h2 id="pipeline">How the pipeline works</h2>
  <ol>
    <li><strong>Push:</strong> a change is pushed to the <code>main</code> branch.</li>
    <li><strong>CI:</strong> GitHub Actions builds the Docker image and pushes it to Docker Hub with a unique tag.</li>
    <li><strong>Tag update:</strong> the workflow updates the image tag in the Helm <code>values.yaml</code> and commits it back to the repo.</li>
    <li><strong>CD:</strong> Argo CD detects the new commit and syncs the updated chart to the EKS cluster.</li>
    <li><strong>Traffic:</strong> users reach the app through Route 53, which points to the load balancer created by the Ingress.</li>
    <li><strong>Monitoring:</strong> Prometheus scrapes metrics and Grafana shows them on dashboards.</li>
  </ol>

  <h2 id="prereq">Prerequisites</h2>
  <ul>
    <li>AWS account with the AWS CLI configured</li>
    <li><code>kubectl</code>, <code>helm</code>, <code>eksctl</code> (or the tool you used to create the cluster), and Docker installed</li>
    <li>Docker Hub account</li>
    <li>GitHub repository secrets for the CI pipeline: <span class="fill">use the secret names from your workflow file</span></li>
    <li>A domain in Route 53 (optional)</li>
  </ul>

  <h2 id="setup">Setup</h2>

  <h3>1. Clone the repo</h3>
<pre>git clone https://github.com/JANAPRIYA-Bme/go-web-app.git
cd go-web-app</pre>

  <h3>2. Run locally with Docker</h3>
<pre>docker build -t &lt;dockerhub-username&gt;/go-web-app:v1 .
docker run -p 8080:8080 &lt;dockerhub-username&gt;/go-web-app:v1</pre>
  <p>Open <code>http://localhost:8080</code>.</p>

  <h3>3. Create the EKS cluster</h3>
<pre>eksctl create cluster --name &lt;cluster-name&gt; --region &lt;region&gt; --nodes 2</pre>
  <p><span class="fill">Replace with the exact command or method you used.</span></p>

  <h3>4. Install the Ingress controller</h3>
  <p><span class="fill">Add the commands you used, for example NGINX Ingress or the AWS Load Balancer Controller.</span></p>

  <h3>5. Deploy with Helm (manual check)</h3>
<pre>helm install go-web-app ./helm/go-web-app-chart
kubectl get pods
kubectl get ingress</pre>

  <h3>6. Install Argo CD and create the application</h3>
<pre>kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml</pre>
  <p>Create an Argo CD Application that points to <code>helm/go-web-app-chart</code> in this repo, with auto-sync enabled.</p>

  <h3>7. Configure DNS</h3>
  <p>Point a Route 53 record to the load balancer address shown by <code>kubectl get ingress</code>.</p>

  <h3>8. Install monitoring</h3>
<pre>helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring --create-namespace</pre>
  <p>Use <code>kubectl port-forward</code> to open Grafana and view the dashboards.</p>

  <h3>9. Clean up to avoid AWS charges</h3>
<pre>helm uninstall go-web-app
eksctl delete cluster --name &lt;cluster-name&gt; --region &lt;region&gt;</pre>

  <h2 id="screens">Screenshots</h2>
  <div class="shots">
    <div class="shot">GitHub Actions run<br><code>images/actions.png</code></div>
    <div class="shot">Argo CD synced app<br><code>images/argocd.png</code></div>
    <div class="shot">App running in browser<br><code>images/app.png</code></div>
    <div class="shot">Grafana dashboard<br><code>images/grafana.png</code></div>
  </div>
  <p style="margin-top:10px;color:var(--muted);font-size:.92rem;">Replace each box with your real screenshot and delete the ones you don't have.</p>

  <h2 id="learned">Challenges and what I learned</h2>
  <ul>
    <li><span class="fill">Write a real problem you hit, for example the tag-update commit needing a rebase before pushing, and how you fixed it.</span></li>
    <li><span class="fill">Write something you learned about GitOps or Kubernetes networking.</span></li>
  </ul>

  <h2 id="future">Future improvements</h2>
  <ul>
    <li>Provision the VPC and EKS cluster with Terraform</li>
    <li>Add image vulnerability scanning to the CI pipeline</li>
    <li>Add Grafana alerts</li>
    <li>Add HTTPS with cert-manager</li>
  </ul>

  <footer>
    <strong>Janapriya M</strong><br>
    <a href="https://www.linkedin.com/in/janapriya-m">LinkedIn</a> ·
    <a href="https://github.com/JANAPRIYA-Bme">GitHub</a> ·
    <a href="mailto:janapriyabme03@gmail.com">janapriyabme03@gmail.com</a>
    <p style="margin-top:12px;">Original application: <a href="https://github.com/iam-veeramalla/go-web-app">iam-veeramalla/go-web-app</a>. See the <code>LICENSE</code> file for license terms.</p>
  </footer>

</main>
</body>
</html>
