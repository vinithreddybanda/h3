# Contact Form Project

This project contains a simple contact form (`index.html`), instructions for pushing to GitHub, a Jenkins pipeline with `pollSCM`, and an Ansible playbook for deploying `index.html`.

---

## 1. Contact Form (`index.html`)

Create a file named `index.html` with the following code:

```html
<!-- filepath: index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contact Form</title>
</head>
<body>
    <h2>Contact Us</h2>
    <form>
        <label for="name">Name:</label><br>
        <input type="text" id="name" name="name" required><br><br>

        <label for="email">Email:</label><br>
        <input type="email" id="email" name="email" required><br><br>

        <label for="mobile">Mobile Number:</label><br>
        <input type="tel" id="mobile" name="mobile" required><br><br>

        <label for="subject">Subject:</label><br>
        <input type="text" id="subject" name="subject" required><br><br>

        <input type="submit" value="Submit">
    </form>
</body>
</html>
```

---

## 2. Push to GitHub

### Step-by-step:

1. **Initialize Git:**
   ```sh
   git init
   ```

2. **Add files:**
   ```sh
   git add index.html
   ```

3. **Commit:**
   ```sh
   git commit -m "Add contact form"
   ```

4. **Create a GitHub repository:**
   - Go to [GitHub](https://github.com), create a new repository (e.g., `contact-form`).

5. **Add remote:**
   ```sh
   git remote add origin https://github.com/yourusername/contact-form.git
   ```

6. **Push:**
   ```sh
   git push -u origin master
   ```

---

## 3. Jenkins Pipeline with `pollSCM`

Create a file named `Jenkinsfile`:

```groovy
// filepath: Jenkinsfile
pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *') // Polls every 5 minutes
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'No build steps required for HTML.'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Ready for deployment.'
            }
        }
    }
}
```

---

## 4. Ansible Playbook for `index.html`

Create a file named `deploy.yml`:

```yaml
# filepath: deploy.yml
- name: Deploy index.html to web server
  hosts: webservers
  become: yes
  tasks:
    - name: Copy index.html to /var/www/html/
      copy:
        src: index.html
        dest: /var/www/html/index.html
        mode: '0644'
```

**Inventory example (`hosts`):**
```ini
[webservers]
your_web_server_ip_or_hostname
```

**Run the playbook:**
```sh
ansible-playbook -i hosts deploy.yml
```

---

## 5. Summary

- `index.html`: Contact form with name, email, mobile, subject.
- Pushed to GitHub following standard git commands.
- Jenkins pipeline (`Jenkinsfile`) with `pollSCM` for auto-build.
- Ansible playbook (`deploy.yml`) to deploy `index.html` to web server.

---

## References

- [GitHub Docs](https://docs.github.com/)
- [Jenkins Pipeline](https://www.jenkins.io/doc/book/pipeline/)
- [Ansible Playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html)