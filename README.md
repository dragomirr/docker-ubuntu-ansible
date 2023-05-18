# Ubuntu Ansible Test Images

Ubuntu container images for Ansible playbook and role testing.

## Tags

  - `18.04`, `20.04`, `22.04` -- tags resemble ubuntu version
  - `latest` -- latest ubuntu lts release

## How to Build

This image is pushed to Docker Hub, but if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/install/).
  2. Run `docker build -t docker-ubuntu-ansible:22.04 .` -- to create image using ubuntu 22.04 which is default.
  3. To create image with different ubuntu version run `docker build -t docker-ubuntu-ansible:20.04 . --build-arg UBUNTU_VERSION=20.04`

> Note: Switch between `master` and `testing` depending on whether you want the extra testing tools present in the resulting image.

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull dockemir/docker-ubuntu-ansible:latest` (or use the image you built earlier, e.g. `ubuntu-ansible:22.04`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:rw --cgroupns=host dockemir/docker-ubuntu-ansible:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!

## Author

Created in 2018 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).

Updated by `dragomirr` in 2023.
