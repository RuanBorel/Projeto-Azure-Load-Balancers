# Projeto-Azure-Load-Balancers
Laboratório prático de criação de balanceadores de carga no Azure (Load Balancer e Application Gateway)

# Projeto: Azure Load Balancer - Standard Load Balancer & Application Gateway

Este repositório contém meu laboratório prático sobre os serviços de balanceamento de carga no Microsoft Azure, com foco em estudo para certificações e aplicação de conhecimento em ambiente real.

Foram explorados e configurados dois tipos de balanceadores:
- Azure Standard Load Balancer (Camada 4 - TCP/UDP)
- Azure Application Gateway (Camada 7 - HTTP/HTTPS)

---
# 📌 Objetivo do Projeto

- Entender na prática o funcionamento dos balanceadores de carga no Azure
- Criar uma topologia funcional com VMs e serviços WEB
- Validar conceitos de Camada 4 x Camada 7
- Validar Funcionamento de tráfego seguro HTTPS usando domínio personalizado
- Gerar certificado SSL e configurar Listner HTTPS
- Criar redirecionamento automático HTTP → HTTPS
- Estudar recursos exigidos na *certificação AZ-104*
- Documentar o passo a passo e processos para compartilhar conhecimento no Linkedin e GitHub

---

# 🗺 Arquitetura criada 

<img width="916" height="567" alt="Arquitetura Loadbalancers" src="https://github.com/user-attachments/assets/a8e16c75-ac2a-4d0d-b2f8-2b9e1848a4aa" />

---

### 🟦 Standard Load Balancer
- 2 VMs Windows - Backend Pool
- Health Probe configurado na porta 80
- Load Balanceing Rule redirecionando tráfego público para as VMs
- Análise de sessçao e comportamento Round-Robin

### 🟩 Application Gateway
- 2 VMs Windows
- Domínio Personalizado configurado
- Certificado SSL carregado para Listener HTTPS
- Redirecionamento HTTP → HTTPS no Listner
- Frontend IP público
- Listner, Backend Pool, probes e HTTP Settings configurados
- Demonstração de Path-based routing
- Teste de Hostname e regras de roteamento por URL

# 🌐 Configuração do Domínio & HTTPS
|  Item |  Status  |
|-------|----------|
| Dominio Personalizado configurado|  ✔  |
| Certificado SSL criado (PFX) |  ✔  |
| Listner HTTPS usando certificado |  ✔  
| Redirecionamento HTTP → HTTPS |  ✔   |

Fluxo HTTPS
1. Usuário acessa http://conectaredes.cloud
2. Application Gateway redireciona automaticamente para https://conectaredes.cloud
3. Certificado valida o tráfego e HTTPS é estabelecido
4. Tráfego é encaminhado ao Backend Pool

---

# 🧪 Ambiente Utilizado
| Componente | Quantidade | Finalidade |
|------------|------------|------------|
| Resouce Group|     1    | Organização |
| Virtual Network |    1   | Comunicação Interna |
|    Subnets      |    3   | App Gateway / Vms / LoadBalancer |
|  VMs Windows    |    4   | Backend dos balanceadores |
| Application Gateway |   1   |  Balanceamento camada 7 |
| Standard LoadBalancer |  1  |  Balancemanto camada 4  | 
| Certificado SSL |  1  | Tráfego criptografado  |
| Domínio personalizado |   1   |  Testes reais em HTTPS  |

# 🧭 Passo a Passo de Configuração

1 Criação da Infraestrutura
- Criar RG, VNET Subnets
- Criar as VMs do Backend Pool
- Criar NSGs para as Subnets
- Criar ASGs para as VMs

2 Certificado & Domínio
- Criado certificado SSL (Key + CRT → PFX)
- Adicionado registro A no DNS Público apontando para o IP Público do App Gateway
- Upload do certificado via Portal

3 Standard LoadBalancer
- Criar IP Público
- Criar Load Balancer
- Criar o Backend Pool
- Associar VMs ao Backend Pool
- Criar o Health Probe
- Criar a Rule do Load Balancer
- Fazer os testes

3 Application Gateway
- Criar IP Público
- Criar Application Gateway
- Criar Listner e HTTP/HTTPS Settings
- Configurar certificado SSL no Listner HTTPS
- Criar redirecionamento HTTP → HTTPS
- Configurar certificado SSL no Listner
- Configurar Backend Pool
- Associar rotas de testes
- Fazer os testes

# 🧪 Testes Realizados
|   Teste   |  Resultado Esperado  | Status  |
|-----------|----------------------|---------|
| Acesso HTTP sem criptografia | Redirecionar para HTTPS |  ✔  |
| Acesso HTTPS via domínio personalizado | Cadeia de certificado válida e cadeado ativo |  ✔  |
| Derrubar VM backend | Remover do Pool automaticamente |  ✔  |

---

# 📌 Status do Projeto
100% - Finalizado com HTTPS e domínio personalizado

---

## 🧑‍💻 Autor

**Ruan Carlos Eduardo Borel**
Azure Administrator (em preparação – AZ-104)  
LinkedIn: www.linkedin.com/in/ruan-borel-198806185
GitHub: https://github.com/RuanBorel
