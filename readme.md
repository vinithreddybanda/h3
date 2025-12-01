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

## 4. Ansible Playbook for `index.html` (WSL Ubuntu & Local)

### Using WSL Ubuntu (Recommended for Windows users)

1. **Install WSL and Ubuntu:**  
   Follow [Microsoft’s guide](https://learn.microsoft.com/en-us/windows/wsl/install) to install WSL and Ubuntu.

2. **Install Ansible in Ubuntu:**
   ```sh
   sudo apt update
   sudo apt install ansible
   ```

3. **Prepare your files:**  
   Place `index.html`, `deploy.yml`, and `hosts` in your project directory.

4. **Inventory file (`hosts`):**
   ```ini
   [webservers]
   localhost
   ```

5. **Playbook (`deploy.yml`):**
   ```yaml
   # filepath: deploy.yml
   - name: Deploy index.html to web server
     hosts: webservers
     connection: local
     become: yes
     tasks:
       - name: Ensure /var/www/html exists
         file:
           path: /var/www/html
           state: directory
           mode: '0755'
       - name: Copy index.html to /var/www/html/
         copy:
           src: index.html
           dest: /var/www/html/index.html
           mode: '0644'
   ```

6. **Run the playbook:**
   ```sh
   ansible-playbook -i hosts deploy.yml
   ```

---

### Using Local Ubuntu (Native Linux)

Follow the same steps as above.  
If you want to deploy to a remote server, replace `localhost` in the `hosts` file with the server’s IP or hostname and ensure SSH access.

---

## 5. Summary

- `index.html`: Contact form with name, email, mobile, subject.
- Pushed to GitHub following standard git commands.
- Jenkins pipeline (`Jenkinsfile`) with `pollSCM` for auto-build.
- Ansible playbook (`deploy.yml`) to deploy `index.html` to web server using WSL Ubuntu or local Ubuntu.

---

## References

- [GitHub Docs](https://docs.github.com/)
- [Jenkins Pipeline](https://www.jenkins.io/doc/book/pipeline/)
- [Ansible Playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html)
- [WSL Installation Guide](https://learn.microsoft.com/en-us/windows/wsl/install)