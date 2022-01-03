# Open Source CI/CD Secrets Management with Amber

- Better tools. Better productivity

Normally in GitHub/Gitlab etc, you'd have to create an entry for every secret, per environment,
and keep updating these. This does not scale.

You could use your CI/CD's secrets apis (if it exists), but there's a better
way.

With amber, you only need to store **one** secret per environment, *and* they're
version tracked.

Another bonus is that it's the same process regardless of which CI/CD pipeline tool your using
(GitHub, GitLab, concourse ci, Jenkins) it's the same pattern, reducing lock-in to your CI/CD system.

Finally, since secrets are securly stored in the repo, they are versioned. 

### Praise / ah-ha! moments 💡

> "Damn, I forgot to update the CI/CD secrets and my build is failing."

With amber your secrets are version controlled alongside your code.

> "Help! I'm debugging my pipeline, I wish I could securly decrypt my CI/CD secrets to troubleshoot my issue."

With amber you can securly decrypt your secrets.

> "That would be useful for updating and maintaining the secrets because it gets confusing with so many secrets."

Every CI/CD system has a different interface, amber reduces the compexity with [only one](https://xkcd.com/927/) place to manage such secrets.

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
