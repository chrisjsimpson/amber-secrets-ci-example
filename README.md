# Open Source CI/CD Secrets Management with Amber

- Better tools.

## Setup

### Install amber

[Install amber instructions](https://github.com/fpco/amber#install).

If on x86_64 linux:

```
curl -L https://github.com/fpco/amber/releases/download/v0.1.1/amber-x86_64-unknown-linux-musl > amber
chmod +x amber
sudo mv amber /usr/local/sbin/
```

### Generate staging secret key (aka `AMBER_SECRET`)

Use the `amber` cli to create a secret key and yaml file for each environment.

e.g. here we create a staging and production file:

> Remember to store your secret key elsewhere for each environment, since you'll never be shown it again. Recommendation: keep it in a password manager.

#### Create amber-staging.yaml

```
amber init --amber-yaml amber-staging.yaml
```

**Important**: Copy the secret key to you password manager.

#### Create amber-production.yaml

```
amber init --amber-yaml amber-production.yaml
```

**Important again**: Copy the secret key for production to you password manager.


### Set up envrionments (Github CI/CD)

Normally in GitHub you'd have to create an entry for every secret, per environment- this
does not scale.

With amber, you only need to store **one** secret per environment.

Another bonus is it's the same process regardless of which CI/CD pipeline tool your using
(GitHub, GitLab, concourse ci, Jenkins) it's the same pattern.

Finally, since secrets are securly stored in the repo, they are versioned. 

## Detailed step-by-step how to create environments & add secrets in GitHub
<details>
  <summary>
  Detailed Github CI steps with images
  </summary>

  ![Create github environment](./images/github/create-environments.png)

  Crate staging environment
  ![Create staging environment](./images/github/create-staging-environment.png)

  Add secret
  ![Add a secret](./images/github/staging-environment-add-secret.png)


  Add the `AMBER_SECRET` you generated from the `amber` cli
  ![Add amber secret](./images/github/staging-environment-add-secret-amber-secret.png)

  Verify `AMBER_SECRET` secret saved to environment.
  ![Add amber secret](./images/github/staging-environment-add-secret-amber-secret-saved.png)

  ## References

  [FP Complete Reduces Your Time To Market With Advanced Software Engineering
  ](https://www.youtube.com/watch?v=1G3FYZEM18U)
</details>
