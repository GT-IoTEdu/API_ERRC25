
# 🚀 API-IoT-EDU

  

Sistema integrado para gerenciamento seguro de dispositivos IoT em ambientes acadêmicos, combinando autenticação federada via CAFe, gerenciamento automatizado de regras no pfSense e monitoramento inteligente de tráfego com detecção automática de ameaças.

  

## 📋 Sobre o Sistema

  

O **API-IoT-EDU** é uma plataforma completa desenvolvida para atender às demandas de segurança, governança e escalabilidade das redes acadêmicas nacionais. Diferente de todas as soluções existentes, o sistema unifica em uma única plataforma integrada:

  

- ✅ **Gerenciamento de Dispositivos IoT**: Cadastro, edição e monitoramento de dispositivos com sincronização automática entre banco de dados e pfSense

- 🔐 **Autenticação Federada**: Integração com CAFe (SAML 2.0/OAuth2), Google OAuth2 e login administrativo

- 🛡️ **Bloqueio Automático**: Detecção automática de ameaças via Zeek Network Security Monitor e bloqueio proativo através de integração nativa com firewall (pfSense)

- 📊 **Gestão Multi-Institucional**: Suporte a múltiplas instituições e campi com controle granular de permissões

- 🔄 **Atribuição Automática de IP**: Sistema de DHCP integrado para gerenciamento de endereços IP

- 📈 **Dashboard Administrativo**: Interface web moderna com três níveis de acesso (Usuário, Gestor, Administrador)

  

## 🏗️ Arquitetura

  
![Diagrama de Arquitetura do Sistema](https://raw.githubusercontent.com/JonerMello/COVID19/refs/heads/master/APIIoTV1.png)
O sistema é composto por:

  

-  **Backend**: API REST desenvolvida em FastAPI (Python) com integração MySQL

-  **Frontend**: Interface web desenvolvida em Next.js 15.2 com React 19 e TypeScript

-  **Integrações**:

- pfSense API v2 (gerenciamento de firewall e DHCP)

- Zeek Network Security Monitor (análise de tráfego e detecção de ameaças)

- CAFe (autenticação federada acadêmica)

  

## 📦 Pré-requisitos

  

### Backend

- Python 3.9 ou superior

- MySQL 5.7+ ou MariaDB 10.3+

- OpenSSL (para certificados SAML)

- pfSense com API REST habilitada

- Zeek Network Security Monitor (opcional, para detecção de ameaças)

  

### Frontend

- Node.js 18+ ou superior

- npm, yarn ou pnpm

  

## 🚀 Instalação

  

### 1. Clonar o Repositório

  

```bash

git  clone  https://github.com/GT-IoTEdu/API_ERRC25.git

cd  API_ERRC25

```

  

### 2. Instalação do Backend

  

#### 2.1. Criar ambiente virtual (recomendado)

  

```bash

cd  backend

python  -m  venv  venv

  

# Windows

venv\Scripts\activate

  

# Linux/Mac

source  venv/bin/activate

```

  

#### 2.2. Instalar dependências

  

```bash

pip  install  -r  requirements.txt

```

  

#### 2.3. Configurar variáveis de ambiente

  

Copie o arquivo de exemplo e configure as variáveis:

  

```bash

cp  env_example.txt  .env

```

  

Edite o arquivo `.env` com suas configurações:

  

```env

# Configurações do banco de dados MySQL

MYSQL_USER=IoT_EDU

MYSQL_PASSWORD=sua_senha_mysql_aqui

MYSQL_HOST=localhost

MYSQL_DB=iot_edu

  

# Configurações de autenticação CAFe (OAuth2/OpenID Connect)

CAFE_CLIENT_ID=seu_client_id_cafe_aqui

CAFE_CLIENT_SECRET=seu_client_secret_cafe_aqui

CAFE_AUTH_URL=https://sso.cafe.unipampa.edu.br/auth/realms/CAFe/protocol/openid-connect/auth

CAFE_TOKEN_URL=https://sso.cafe.unipampa.edu.br/auth/realms/CAFe/protocol/openid-connect/token

CAFE_USERINFO_URL=https://sso.cafe.unipampa.edu.br/auth/realms/CAFe/protocol/openid-connect/userinfo

CAFE_REDIRECT_URI=http://localhost:8000/api/auth/cafe/callback

  

# Configurações da API do pfSense

PFSENSE_API_URL=https://seu-pfsense.local/api/v2/

PFSENSE_API_KEY=sua_api_key_pfsense_aqui

  

# Configurações JWT para SAML

JWT_SECRET_KEY=sua_chave_secreta_jwt_muito_segura_aqui

  

# Configurações do Zeek Network Security Monitor

ZEEK_API_URL=http://192.168.100.1/zeek-api

ZEEK_API_TOKEN=seu_token_zeek_aqui

  

# Configurações de atribuição automática de IP

IP_RANGE_START=192.168.100.1

IP_RANGE_END=192.168.100.254

IP_RANGE_EXCLUDED=192.168.100.1,192.168.100.100,192.168.100.200

  

# Configurações de acesso administrativo

ADMIN_ACCESS=admin@iotedu.local

ADMIN_PASSWORD=admin123

```

  

#### 2.4. Criar banco de dados

  

Crie o banco de dados MySQL:

  

```sql

CREATE  DATABASE iot_edu CHARACTER  SET utf8mb4 COLLATE utf8mb4_unicode_ci;

CREATE USER 'IoT_EDU'@'localhost' IDENTIFIED BY  'sua_senha_mysql_aqui';

GRANT ALL PRIVILEGES ON iot_edu.*  TO  'IoT_EDU'@'localhost';

FLUSH PRIVILEGES;

```

  

#### 2.5. Inicializar tabelas do banco de dados

  

```bash

python  -m  db.create_tables

```

  

### 3. Instalação do Frontend

  

#### 3.1. Instalar dependências

  

```bash

cd  ../frontend

npm  install

# ou

yarn  install

# ou

pnpm  install

```

  

#### 3.2. Configurar variáveis de ambiente

  

Crie um arquivo `.env.local` na pasta `frontend/`:

  

```env

NEXT_PUBLIC_API_URL=http://localhost:8000

```

  

> **Nota**: Ajuste a URL da API conforme necessário para seu ambiente.

  

## ▶️ Execução

  

### Executar o Backend

  

No diretório `backend/`:

  

```bash

# Ativar ambiente virtual (se estiver usando)

# Windows: venv\Scripts\activate

# Linux/Mac: source venv/bin/activate

  

# Executar servidor de desenvolvimento

python start_server.py

  


```

  

O backend estará disponível em: `http://localhost:8000`

  

- Documentação interativa (Swagger): `http://localhost:8000/docs`

- Documentação alternativa (ReDoc): `http://localhost:8000/redoc`

  

### Executar o Frontend

  

No diretório `frontend/`:

  

```bash

# Modo desenvolvimento

npm  run  dev


```

  

O frontend estará disponível em: `http://localhost:3000`

  



## 📚 Documentação Adicional

  

-  **Documentação da API**: Acesse `/docs` após iniciar o backend

-  **Documentação do Backend**: Consulte `backend/docs/`

-  **Documentação do Frontend**: Consulte `frontend/docs/`

-  **Guia de Deploy**: Consulte `backend/deploy/`

  

## 🔧 Funcionalidades Principais

  

### Autenticação e Autorização


- Autenticação Google OAuth2

- Login administrativo 

- Controle de permissões baseado em níveis (USER, MANAGER, ADMIN)

  

### Gerenciamento de Dispositivos

- Cadastro e gerenciamento de dispositivos IoT

- Atribuição de dispositivos a usuários

- Sincronização automática com pfSense

- Validação de IP/MAC e faixas autorizadas

  

### Integração pfSense

- Gerenciamento de aliases DHCP

- Mapeamentos estáticos DHCP

- Configuração de regras de firewall

- Aplicação automática de bloqueios

  

### Monitoramento e Segurança

- Integração com Zeek Network Security Monitor

- Detecção automática de ameaças

- Bloqueio automático de dispositivos maliciosos

- Sistema de feedback para bloqueios

- Histórico de incidentes de segurança

  

## 🔗 Links Úteis

  

-  **Repositório**: [https://github.com/GT-IoTEdu/API_ERRC25](https://github.com/GT-IoTEdu/API_ERRC25)

-  **Documentação CAFe**: [https://www.cafeexpresso.rnp.br/](https://www.cafeexpresso.rnp.br/)

-  **pfSense**: [https://www.pfsense.org/](https://www.pfsense.org/)

-  **Zeek**: [https://zeek.org/](https://zeek.org/)

  

## ⚠️ Notas Importantes

  

- Certifique-se de que o pfSense tenha a API REST habilitada e configurada corretamente

- Para produção, altere todas as senhas padrão e chaves secretas

- Configure adequadamente as variáveis de ambiente conforme seu ambiente

- O sistema requer acesso de rede ao pfSense e ao Zeek (se utilizado)

  

  

