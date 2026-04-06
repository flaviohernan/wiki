# SSH

# Criando chave RSA

Abrir o terminal e executar o comando abaixo, substituindo pelo seu e-mail: 

```console
ssh-keygen -t ed25519 -C "email@exemplo.com"
```
Quando for solicitado "Enter a file in which to save the key" colocar o caminho onde 
o arquivo da chave será salvo.

Após gerar o par de chaves (pública e privada), você deve adicionar a chave pública à sua conta: 

Copie sua chave pública:
No Linux/Mac: cat ~/.ssh/id_ed25519.pub
No Windows (Git Bash): cat ~/.ssh/id_ed25519.pub

Copie todo o conteúdo exibido, começando com ssh-ed25519.


# Adicionando no cliente ssh
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

# Adicionando no Servidor ssh

Verificar se a chave publica, conteúdo do arquivo id_ed25519.pub está listado
em **~/.ssh/authorized_keys**, caso contrário é necessário copiar para dentro desse arquivo.

# Acessando o computador remoto

# Referencias
### https://askubuntu.com/questions/311558/ssh-permission-denied-publickey#:~:text=There%20are%20several%20reasons%20why%20you%20might,and%20the%20files%20within%20are%20600%20permissions
