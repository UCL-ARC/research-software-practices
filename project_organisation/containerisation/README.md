# Containerisation

Containerisation wraps your software with all its dependencies into a standardised, portable unit. This ensures your
code runs consistently across different computing environments, from laptops to HPC clusters to cloud platforms.

## Why containerise?

- 🔒 **Reproducibility**: Freeze your software environment, making results reproducible months or years later
- 🚀 **Portability**: Run your software anywhere containers are supported, without worrying about local dependencies
- 🧪 **Isolation**: Avoid conflicts between different projects' dependencies
- 🤝 **Collaboration**: Share a complete working environment with collaborators, not just code
- 📦 **Deployment**: Simplify deployment to production systems, HPC clusters, or cloud services

## Docker

[Docker](https://www.docker.com/) is the most widely-used containerisation platform and our recommended starting point
for most projects.

### Creating a Dockerfile

A `Dockerfile` defines your container image. Start with a minimal base image appropriate for your language:

```dockerfile
# For Python projects
FROM python:3.11-slim

WORKDIR /app

# Copy dependency files first (for better caching)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Run your application as a non-root user
USER appuser
CMD ["python", "main.py"]
```

### Best practices for Dockerfiles

- **Use official base images**: Start from official language images (e.g., `python:3.11`, `r-base:4.3`, `gcc:13`)
- **Minimise layers**: Combine related `RUN` commands to reduce image size
- **Leverage build cache**: Copy dependency files before source code so dependencies aren't reinstalled on every code
  change
- **Use `.dockerignore`**: Exclude unnecessary files (similar to `.gitignore`) to speed up builds
- **Don't run as root**: Create a non-root user for better security
- **Pin versions**: Specify exact versions of base images and dependencies for reproducibility, i.e. do not use `latest`
- **Multi-stage builds**: Use [separate build and runtime](https://docs.docker.com/build/building/multi-stage/) stages
  to minimise final image size

### Building and running containers

```sh
# Build an image
docker build -t my-project:latest .

# Run a container
docker run my-project:latest

# Run interactively
docker run -it my-project:latest /bin/bash

# Mount local data
docker run -v /path/to/data:/data my-project:latest
```

### Sharing Docker images

Once you have built an image, you can make it available to others by pushing it to a registry. There are many options to
do this. Here are some popular ones:

- [**Docker Hub**](https://hub.docker.com/): Public registry for sharing images (free for public repositories)
- [**GitHub Container Registry**](https://docs.github.com/en/packages/quickstart): Integrated with GitHub, good for
  projects already on GitHub
- **Cloud provider registries**: e.g. [Amazon Elastic Container Registry](https://aws.amazon.com/ecr/) or
  [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) are useful for applications
  that need to be deployed on cloud platforms

The advantage of using container registries is that they provide a centralised location for storing and sharing images,
making it easier to manage and deploy applications across different environments. They also offer features like image
versioning, security scanning, and automated builds, which can help ensure the reliability and security of your
applications.

## Singularity/Apptainer

Many HPC systems don't allow Docker due to security concerns. [Singularity](https://sylabs.io/singularity/) (now also
known as [Apptainer](https://apptainer.org/)) is designed for HPC environments and is our recommendation for those
contexts.

### Key differences from Docker

- Runs without root privileges (safer for shared systems)
- Better integration with HPC schedulers
- Can run Docker images directly
- Uses a single-file image format (easier to share via filesystem)

### Converting Docker to Singularity

```sh
# Build from Docker Hub
singularity build my-image.sif docker://my-username/my-project:latest

# Build from a Dockerfile
singularity build my-image.sif docker-daemon://my-project:latest

# Run a Singularity container
singularity run my-image.sif

# Execute a command
singularity exec my-image.sif python script.py
```

### Definition files

For more control, create a Singularity definition file (`*.def`):

```singularity
Bootstrap: docker
From: python:3.13-slim

%files
    requirements.txt /app/requirements.txt
    . /app

%post
    cd /app
    pip install --no-cache-dir -r requirements.txt

%runscript
    cd /app
    exec python main.py
```

## When to containerise

Containerisation adds complexity, so consider whether it's appropriate for your project:

### Good use cases

- Deploying web services or APIs
- Complex dependency chains (especially mixing languages or system libraries)
- Sharing computational environments for reproducible research
- Running on HPC or cloud infrastructure
- Projects with multiple contributors using different operating systems

### When simpler alternatives might suffice

- Simple scripts with few dependencies
- Internal tools used only on your own machine
- Prototyping and early development (containerise later when things stabilise)
- When language-specific virtual environments (e.g., Python's `venv`, R's `renv`) meet your needs

## Further reading

- [Docker documentation](https://docs.docker.com/)
- [Apptainer documentation](https://apptainer.org/docs/)
- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Containers for computational reproducibility](https://www.nature.com/articles/s43586-023-00236-9) (Nature article)
- [Introduction to Singularity](https://carpentries-incubator.github.io/singularity-introduction/) (Carpentries lesson)
