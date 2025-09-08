# O que o código faz:

### Sobe um servidor local na porta 8080.

- Mostra uma página Kanban no navegador em http://localhost:8080

- API REST para tarefas:

- GET /api/tasks → lista todas.

- POST /api/tasks → cria nova.

- PATCH /api/tasks/{id}/status → muda status (To-Do, Doing, Done).

- DELETE /api/tasks/{id} → apaga.

- Salva os dados em um arquivo CSV (data_tasks.csv) e carrega de lá quando reinicia.

- Interface simples: você adiciona, move e exclui tarefas direto no navegador.

---
# Kanban Local (Java + HTTP Server)

Este projeto é um protótipo simples de quadro Kanban implementado em **Java puro**, usando o `HttpServer` embutido no JDK.  
Ele serve uma página HTML estática e expõe uma API REST para gerenciar tarefas (CRUD).  
As tarefas são persistidas em um arquivo CSV local.

---

## 🚀 Como executar

### Pré-requisitos:
- **Java JDK 17+** instalado.
  
[Clique aqui para baixar](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)

Verifique com:
```bash
java -version
javac -version
```

---


## 1. Pontos Positivos:

- Funcional: o código realmente entrega um quadro Kanban local, com frontend simples e API REST completa (CRUD de tarefas).

- Sem dependências externas: usa apenas o que vem no próprio JDK (HttpServer e classes básicas de I/O). Isso facilita rodar em qualquer lugar.

- Organização mínima: já tem separação de handlers (RootHandler, ApiTasksHandler), funções utilitárias, persistência em arquivo, etc.

- Persistência simples: salva em CSV e carrega de volta — não é robusto, mas garante que os dados não se percam quando reinicia.

- Frontend decente: HTML embutido é leve, funciona e tem recursos básicos (adicionar, mover, excluir).



## 2. Pontos Negativos:

- Classe única gigante: tudo está dentro de App.java, o que deixa difícil de manter e entender (já está com ~400 linhas).

- Uso de arrays fixos (MAX=5000): pouco flexível; seria melhor usar coleções (ArrayList, Map) que crescem sozinhas.

- JSON manual: parse e serialização feitos “na unha” (jsonGet, toJsonTask), o que é frágil e limitado. Uma lib como Gson ou Jackson faria isso de forma segura e clara.

- Persistência em CSV: quebra fácil se os dados tiverem caracteres especiais; também não escala bem.

- Sem camadas: tudo (API, lógica, persistência) está misturado. Falta separar em entidades (Task), serviços e controladores.

- Segurança inexistente: qualquer um que acessar o servidor pode criar/editar/excluir tarefas, sem autenticação.

- Testes ausentes: não tem nenhum teste automatizado (JUnit, etc).

---

## Possíveis Melhorias a serem feitas

Refatorar em classes menores (criar uma classe Task e usar listas/coleções em vez de arrays).

Usar Gson/Jackson (simplifica parsing/serialização JSON).

Trocar CSV por SQLite (banco local confiável e fácil de usar).

Organizar em camadas (separar lógica de negócio da API HTTP).

Testes (adicionar pelo menos testes básicos de CRUD).

Frontend (poderia evoluir para um PWA ou usar libs modernas (React/Vue) se a ideia evoluir).

---

### É um bom protótipo didático — simples, direto e funciona. Mas como projeto real, precisaria de refatoração, uso de coleções, biblioteca de JSON e banco de dados. 
Se evoluir para algo maior, a recomendação é migrar para um framework como Spring Boot ou Quarkus e separar bem as camadas.

---

# Proposta de Substituição
Esse projeto atual funciona bem como protótipo, mas pode ser renovado. Um próximo passo seria organizar melhor o código (criando uma classe Task e separando responsabilidades), trocar os arrays manuais por coleções e adotar uma biblioteca de JSON (como Gson ou Jackson). No lugar do CSV, o ideal seria usar um banco simples como SQLite ou IndexedDB para garantir persistência confiável.

Além disso, a interface pode ser aprimorada com recursos de drag-and-drop, atalhos de teclado, filtros e tags, trazendo mais usabilidade.

Dá para evoluir para uma aplicação profissional: um backend com Spring Boot ou Quarkus, banco de dados robusto (PostgreSQL/MySQL), sincronização opcional entre dispositivos (via CRDT), e um frontend moderno (React, Vue ou até PWA instalável). Isso garante escalabilidade, melhor organização e uma experiência de uso comparável a ferramentas de mercado.
