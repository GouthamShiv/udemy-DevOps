# Installing `Jenkins`
---

### Appending `jenkins` key to apt package manager
> wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
> sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

---
---

### Update library and install `jenkins`
> sudo apt-get update
> sudo apt-get install jenkins

---
---