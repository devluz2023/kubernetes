# ☸️ Kubernetes Cluster Orchestration & Cloud-Native Infrastructure

Este repositório centraliza uma coleção completa de manifestos declarativos (`.yaml`) para **Kubernetes**, projetados para provisionar, gerenciar e proteger microsserviços em ambientes de nuvem (*Cloud-Native Architecture*). Os arquivos cobrem desde a segregação de ambientes e ciclo de vida de pods até políticas rigorosas de controle de acesso (RBAC), gerenciamento de dados persistentes, segurança de credenciais e roteamento de tráfego de rede avançado.

---

## 🏗️ Arquitetura dos Manifestos por Camadas Operacionais

Para facilitar a governança do cluster, os componentes estão divididos de acordo com as camadas de arquitetura do ecossistema Kubernetes:

### 🌐 1. Roteamento, Redes & Entrada de Tráfego (Networking)
Manifestos responsáveis por expor as aplicações e gerenciar o tráfego externo para dentro do cluster de forma segura:
* `ingress.yaml` / `api-gateway.yaml`: Configurações de controladores de entrada (Ingress Control) e gateways de API. Gerenciam o roteamento de URL, terminação SSL/TLS e balanceamento de carga na camada 7 (HTTP/HTTPS).
* `loadbalancer.yaml` / `service.yaml`: Abstrações de rede (Camada 4) que expõem os pods internamente ou criam balanceadores de carga públicos integrados nativamente com o provedor de nuvem.

### ⚙️ 2. Ciclo de Vida da Aplicação & Isolamento (Workloads)
* `backend-deployment.yaml`: Define o estado desejado para os microsserviços de backend. Configura estratégias de atualização sem indisponibilidade (*Rolling Updates*), réplicas para alta disponibilidade, limites de recursos (CPU/Memória) e testes de integridade (*Liveness* e *Readiness Probes*).
* `namespace.yaml`: Cria partições lógicas (Namespaces) dentro do cluster para isolar recursos entre diferentes ambientes (ex: Desenvolvimento, Homologação e Produção) ou times.

### 🛡️ 3. Segurança, Governança & Credenciais (Security)
* `rba.yaml` (Role-Based Access Control): Implementação de políticas de privilégio mínimo no cluster. Define *Roles*, *ClusterRoles* e suas respectivas vinculações (*RoleBindings*) para restringir as ações de usuários ou ServiceAccounts.
* `secrets.yaml`: Armazenamento seguro de dados sensíveis criptografados (como strings de conexão, chaves de API e senhas), impedindo a exposição de dados sigilosos no código-fonte da aplicação.

### 🗃️ 4. Persistência de Dados & Armazenamento (Storage)
Manifestos voltados para manter os dados persistidos mesmo após a reinicialização ou destruição de pods:
* `volume.yaml`: Configuração de *PersistentVolumes* (PV) e *PersistentVolumeClaims* (PVC) para alocação e montagem de volumes de armazenamento.
* `storage-account.yaml`: Integração nativa com os serviços de armazenamento gerenciados dos provedores de nuvem para provisionamento dinâmico de discos virtuais ou compartilhamentos de arquivos.

---

## 🛠️ Stack Tecnológica & Conceitos Aplicados

* **Orquestrador Core:** Kubernetes (K8s)
* **Padrão de Configuração:** Manifestos Declarativos em YAML
* **Ecossistemas Cloud Target:** Ambientes gerenciados como Azure Kubernetes Service (AKS) e AWS Elastic Kubernetes Service (EKS).
* **Conceitos de Engenharia:** Alta Disponibilidade, Escalabilidade Horizontal (HPA), Isolamento de Ambientes e Segurança por Design.

---

## 🎯 Impacto de MLOps e Engenharia de Software em Escala

Para indústrias e corporações de grande porte, operar sistemas conteinerizados sem um orquestrador robusto gera gargalos de indisponibilidade e falhas de segurança. Dominar estes recursos habilita a criação de:

1. **Plataformas de MLOps Industriais:** O Kubernetes é a base para ferramentas como Kubeflow e MLflow, permitindo que o treinamento distribuído e o deploy de modelos preditivos rodem de forma elástica e consumam recursos de GPU de forma otimizada.
2. **Arquiteturas Resilientes a Falhas:** Caso um container sofra uma queda por estouro de memória, o Kubernetes o reinicia instantaneamente, garantindo resiliência automática (*Self-Healing*).
3. **Segurança Corporativa Rígida:** O uso combinado de RBAC e Secrets garante conformidade com normas e auditorias internacionais de segurança de TI, restringindo acessos indevidos e protegendo a integridade da infraestrutura.

---
## 🚀 Como Aplicar os Manifestos no Cluster

Certifique-se de possuir a ferramenta de linha de comando `kubectl` instalada e configurada com o contexto do seu cluster ativo:

1. Crie o namespace isolado para o projeto:
   ```bash
   kubectl apply -f namespace.yaml
