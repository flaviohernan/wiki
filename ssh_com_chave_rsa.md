# SSH

# Criando chave RSA

# Adicionando no Host
Verificar se a chave privada foi instalada

```console
ssh-add -l
```
Se houver uma resposta do tipo "The agent has no identities," então será necessário
adicionar uma chave (local onde ficam as chaves ~/.ssh/id_rsa or ~/.ssh/id_ed25519).

```console
ssh-add ~/.ssh/id_ed25519
```

If the agent isn't running, run eval "$(ssh-agent -s)"


Também é importante verificar as permissões de acesso as chaves publicas e privada.

```console
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519  # Your private key
chmod 644 ~/.ssh/id_ed25519.pub # Your public key
```

# Adicionando no Client

# Acessando o computador remoto

# Referencias
### https://askubuntu.com/questions/311558/ssh-permission-denied-publickey#:~:text=There%20are%20several%20reasons%20why%20you%20might,and%20the%20files%20within%20are%20600%20permissions
