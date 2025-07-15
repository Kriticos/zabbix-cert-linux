# 🛠️ Tutorial - Monitoramento de Certificados no Linux com Zabbix Agent 2

## 📁 Estrutura de arquivos

Abaixo um exemplo da estrutura de pasta onde os certificados devem ficar, copie os scripts no servidor docker (Linux com Zabbix Agent 2):

```makefile
/bskp/scripts/zabbix/certificados/
│
├── discover-certs.ps1
└── check_cert_expiry.ps1
```

Os scripts estão configurados para localizar os certificados dentro de um container espefico o container deve ser informado na variavel CONTAINER nos scripts.

## 🔧 2. Configuração do zabbix_agent2.conf

Edite o arquivo zabbix_agent2.conf:

Localize a linha "Userparameter=" e na linha de baixo adicione o conteudo abaixo.

```powershell
# Monitoramento de certificados
UserParameter=cert.lld.nginx,/bskp/scripts/zabbix/certificados/certs-lld.sh
UserParameter=cert.nginx.expira[*],/bskp/scripts/zabbix/certificados/cert-expira.sh $1
```

## 🔧 3. Configuração do Host

Para manter o ambiente organizado, crie um host com o nome “Certificados - Linux” ou outro de sua preferencia.
Em seguida, associe o template “BSKP - Certificados - Linux” e defina o IP do servidor onde os certificados estão instalados.

💡 Essa configuração permite centralizar o monitoramento dos certificados de máquinas específicas com maior clareza e padronização.

## OBSERVAÇÃO

Aconselhavel remover o certificado vencido do servidor, caso contrario ele ficara alertando no painel do zabbix até zerar a data de expiração.
