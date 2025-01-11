# Guia de Configuração: EC2 com Volume EBS

Este projeto demonstra como configurar uma instância EC2 na AWS, anexar um volume EBS e realizar operações básicas de armazenamento. 

---

## Passo 1: Configuração da Instância EC2
1. No Console da AWS, acesse o serviço **EC2**.
2. Crie uma nova instância com a imagem **Amazon Linux 2**.
3. Escolha o tipo de instância, como `t2.micro` para fins de teste.
4. Configure a rede e selecione um grupo de segurança que permita conexões SSH (porta 22).
5. Gere e baixe a chave de acesso (arquivo `.pem`).
6. Finalize a configuração e inicie a instância.

---

## Passo 2: Conexão via SSH
1. Ajuste as permissões da chave privada:
   ```bash
   chmod 400 caminho_para_sua_chave.pem
   ```
2. Conecte-se à instância:
   ```bash
   ssh -i caminho_para_sua_chave.pem ec2-user@IP-da-instancia
   ```

---

## Passo 3: Gerenciamento do Volume EBS
1. No Console da AWS, acesse **Elastic Block Store (EBS)** e crie um volume.
2. Selecione o tamanho do volume (por exemplo, 10 GiB).
3. Anexe o volume à sua instância EC2.

---

## Passo 4: Preparando o Volume
1. Liste os dispositivos conectados:
   ```bash
   lsblk
   ```
2. Formate o volume:
   ```bash
   sudo mkfs.ext4 /dev/xvdf
   ```
3. Crie um ponto de montagem:
   ```bash
   sudo mkdir /mnt/ebs-volume
   ```
4. Monte o volume:
   ```bash
   sudo mount /dev/xvdf /mnt/ebs-volume
   ```
5. Verifique se o volume foi montado:
   ```bash
   df -h
   ```

---

## Passo 5: Trabalhando com Arquivos
1. Altere as permissões do volume para o usuário atual:
   ```bash
   sudo chown ec2-user:ec2-user /mnt/ebs-volume
   ```
2. Navegue até o volume montado:
   ```bash
   cd /mnt/ebs-volume
   ```
3. Crie um arquivo de teste:
   ```bash
   echo "Arquivo criado no volume EBS" > arquivo.txt
   ```
4. Confirme o conteúdo:
   ```bash
   cat arquivo.txt
   ```

---

## Passo 6: Verificações e Encerramento
1. Confira o status do volume:
   ```bash
   ls -l
   df -h
   mount
   ```
2. Desmonte o volume:
   ```bash
   sudo umount /mnt/ebs-volume
   ```
3. Encerre ou interrompa a instância EC2 no Console da AWS para evitar custos adicionais.



