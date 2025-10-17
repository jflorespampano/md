**En construcción**

Si bien el comando git estándar maneja operaciones de control de versiones (como confirmaciones, ramas y fusiones), gh está diseñado específicamente para interactuar con las funciones de GitHub.


Instalar:
```sh
https://github.com/jfloreshotmail/crearRepo.git
```

| Feature                  | Git (Standard)                                                                                             | GitHub CLI (`gh`)                                                                                                                          |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Primary Purpose**      | Manages local/remote Git repositories[](https://docs.github.com/en/github-cli/github-cli/about-github-cli) | Interacts with GitHub features[](https://docs.github.com/en/github-cli/github-cli/about-github-cli)                                        |
| **Repository Workflows** | `git clone`, `git push`                                                                                    | `gh repo clone`, `gh repo create`[](https://cli.github.com/manual/examples)[](https://docs.github.com/en/github-cli/github-cli/quickstart) |
| **Code Review**          | (Limited native support)                                                                                   | `gh pr create`, `gh pr checkout`, `gh pr review`[](https://cli.github.com/)[](https://cli.github.com/manual/examples)                      |
| **Issue Tracking**       | (None)                                                                                                     | `gh issue create`, `gh issue list`[](https://cli.github.com/)[](https://cli.github.com/manual/examples)                                    |
| **GitHub Actions**       | (None)                                                                                                     | `gh run list`, `gh run view`[](https://www.codecademy.com/article/github-cli-tutorial)                                                     |
| **Authentication**       | Often uses SSH keys or credential helpers                                                                  | Uses `gh auth login` or `GITHUB_TOKEN`                                                                                                     |
## **Autenticación**  

Ejecute `gh auth login` en su terminal y siga las instrucciones.