![Ubuntu Linux](https://blogs-images.forbes.com/jasonevangelho/files/2018/07/ubuntu-logo.jpg)

# Deploy and Host Ubuntu Linux on Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/deploy-ubuntu?referralCode=QXdhdr&utm_medium=integration&utm_source=template&utm_campaign=generic)

Get a fully functional Ubuntu 22.04 environment running in the cloud in under a minute. This Railway template deploys Ubuntu with a browser-accessible terminal via [ttyd](https://github.com/tsl0922/ttyd), pre-loaded with Python 3, pip, curl, wget, and git — no SSH client or local setup required.

## About Hosting Ubuntu Linux

Ubuntu is the world's most popular open-source Linux distribution, powering everything from developer workstations to production servers. This template wraps Ubuntu 22.04 LTS in a Docker container and exposes a web-based terminal (ttyd v1.7.3), so you get a full bash shell accessible from any browser.

**Key features:**
- Ubuntu 22.04 LTS base — stable, widely supported, 5-year security updates
- Persistent `/data` volume — files stored here survive redeploys
- Browser terminal via ttyd — no SSH needed
- Pre-installed: `python3`, `pip`, `curl`, `wget`, `git`, `neofetch`
- Password-protected access with configurable credentials

## Persistent Storage

By default, any files you create inside the terminal will be lost on redeploy since containers are stateless. This template includes a `/data` volume — **store anything you want to keep in `/data`**.
```
# Save your work here
cd /data
mkdir myproject
```

Files stored outside `/data` (including your home directory `/root`) will be wiped on every redeploy. Think of `/data` as your personal persistent drive.

## Why Deploy Ubuntu Linux on Railway

Managing a raw VPS means handling OS updates, firewall rules, SSH hardening, and uptime monitoring yourself. Railway removes that overhead:

- **One-click deploy** — no server provisioning or SSH key setup
- **Environment variable UI** — credentials managed securely, never hardcoded
- **Managed infrastructure** — Railway handles networking, restarts, and TLS
- **Instant public URL** — your terminal is reachable over HTTPS immediately
- **Free tier available** — experiment without a credit card

## Common Use Cases

- **Remote development environment** — run scripts, install packages, and test code from any device with a browser
- **Learning Linux** — safe sandboxed Ubuntu shell for students and beginners exploring bash, Python, or system administration
- **CI/CD experimentation** — test shell scripts and automation pipelines in a clean Ubuntu environment
- **Quick Python/scripting tasks** — Python 3 and pip are pre-installed; spin up, run your script, tear down

## Dependencies for Ubuntu Linux

This template has no external service dependencies. Everything runs in a single container.

- [ttyd](https://github.com/tsl0922/ttyd) — web-based terminal emulator (bundled in the Docker image)
- Ubuntu 22.04 base image (`ubuntu:22.04` from Docker Hub)

### Environment Variables Reference

| Variable | Description | Required |
|----------|-------------|----------|
| `PASSWORD` | Password for terminal login. | Yes |
| `USERNAME` | Login username for the terminal.  | Yes |
| `PORT` | Port ttyd listens on inside the container. Default: `8080` | Yes |

### Deployment Dependencies

- **Docker** — the template builds from a Dockerfile in the linked Git repository
- **Railway account** — [railway.app](https://railway.app)
- No database, no object storage, no external APIs required

## Self-Hosting Ubuntu Linux (Outside Railway)

To run this yourself on any machine with Docker:

```
git clone 
cd 
docker build -t ubuntu-ttyd .
docker run -d \
  -p 8080:8080 \
  -e USERNAME=admin \
  -e PASSWORD=yourpassword \
  -e PORT=8080 \
  ubuntu-ttyd
```

Open `http://localhost:8080` in your browser and log in with your credentials.

To install Docker on Ubuntu first:

```
sudo apt update
sudo apt install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo apt update &amp;&amp; sudo apt install -y docker-ce docker-ce-cli containerd.io
```

## Ubuntu Linux vs Alternatives for Cloud Shell / Remote Terminal

| Option | Setup effort | Browser access | Cost |
|--------|-------------|----------------|------|
| **This Railway template** | One click | Yes (ttyd) | Railway infra cost |
| Google Cloud Shell | Zero (managed) | Yes | Free (limited) |
| AWS CloudShell | Zero (managed) | Yes | Free (limited) |
| Raw VPS + ttyd | Manual | Yes | VPS cost + your time |
| VS Code Remote SSH | Moderate | No | VPS cost |

The Railway template wins on **portability and simplicity** — you own the environment, it's not locked to a cloud provider's shell, and you can customize the image freely.

## Getting Started with Ubuntu Linux on Railway

After Railway finishes deploying, click the generated public URL — you'll land on the ttyd login screen. Enter the `USERNAME` and the `PASSWORD` you set in the environment variables. You'll drop straight into a bash shell with neofetch running automatically. From here, install any packages with `apt-get install`, run Python scripts, or use it as a remote scratch environment.

![Ubuntu Linux terminal dashboard screenshot](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/2X/b/ba76cbf3dc8dc2cc94d26dd61c7aad3cedcd5102.png)

## How Much Does Ubuntu Linux Cost?

Ubuntu itself is completely free and open-source — no licensing fees ever. The only cost is infrastructure. On Railway, you pay for compute and memory consumed by the running container, which fits within Railway's free tier for light usage. For heavier workloads, Railway's usage-based pricing applies. There are no paid tiers for Ubuntu itself.

## FAQ

**Q: How do I install Docker on Ubuntu?**  
Add Docker's official GPG key, add the repository to apt sources, then run `sudo apt install docker-ce docker-ce-cli containerd.io`. The full commands are in the self-hosting section above.

**Q: What is Ubuntu used for?**  
Ubuntu runs on desktops, servers, cloud infrastructure, and IoT devices. It's the most widely used Linux distribution for web servers, powering ~47% of Linux-based websites. It's equally popular for developer workstations, CI pipelines, and learning environments.

**Q: Is Ubuntu good for beginners?**  
Yes. Ubuntu is the most beginner-friendly Linux distribution, with extensive documentation, a large community, and long-term support (LTS) releases maintained for 5 years — making it reliable for both learning and production use.

**Q: Can I run this terminal permanently?**  
Yes. As long as your Railway service is running, the ttyd terminal stays accessible. Railway will restart the container automatically if it crashes.

**Q: How do I change the login password?**  
Update the `PASSWORD` environment variable in your Railway service settings. The container will restart and apply the new credentials immediately.

**Q: Is the terminal connection secure?**  
Railway provides HTTPS termination, so the connection to ttyd is encrypted in transit. ttyd itself requires the `USERNAME`/`PASSWORD` credentials you configure.

**Q: How do I keep my files after a redeploy?**  
Store all files you want to persist in the `/data` directory. This is a Railway volume that survives redeploys, container restarts, and crashes. Anything saved outside `/data` — including your home directory `/root` — is ephemeral and will be reset on redeploy.   