# 🗺️ Mapa Digital

Plataforma de **aprendizagem adaptativa** para alunos do **6º ao 9º ano**. Ela combina diagnóstico contínuo, **trilhas de estudo personalizadas por IA**, apoio para tarefas e provas e painéis de acompanhamento para pais, escolas e empresas patrocinadoras.

O projeto nasceu da falta de soluções escaláveis que integrem, num só sistema, o estudo do aluno e o acompanhamento por família e instituições. A proposta é reduzir lacunas de aprendizagem e gerar indicadores para escolas públicas e privadas e para empresas parceiras.

Projeto desenvolvido na **AGES (Agência Experimental de Engenharia de Software) da PUCRS** no 1º semestre de 2026 (março a junho).

## Estrutura do repositório

Este repositório junta os repositórios originais do projeto, com o histórico de commits preservado. O frontend veio do GitLab da AGES e o backend do [GitHub da organização](https://github.com/Mapa-Digital-Ages), onde ele foi desenvolvido:

| Pasta | Descrição | Stack |
|---|---|---|
| [`frontend/`](frontend) | Aplicação web com as áreas de aluno, responsáveis, escola, empresa e administração | TypeScript, React, Vite, Material UI, Jest, Cypress e Playwright |
| [`backend/`](backend) | API REST com autenticação JWT, cadastro e aprovação de usuários, conteúdos, trilhas, uploads e geração de conteúdo por IA | Python 3.12, FastAPI, SQLAlchemy (async), PostgreSQL, Google Gemini, AWS S3, Docker, uv |

## Funcionalidades

O sistema é multiusuário, com uma área para cada perfil:

- **Aluno:** trilha adaptativa, conteúdos, rotina de estudos, envio de tarefas e chat com IA.
- **Responsáveis:** painel de acompanhamento dos alunos vinculados.
- **Escola:** turmas, alunos e pedidos de parceria com empresas.
- **Empresa:** escolas adotadas, parcerias e relatórios.
- **Administração:** gestão de conteúdos, correção de conteúdos, alunos, responsáveis e parcerias.

## Arquitetura

- **Frontend:** organizado por domínios em `src/modules/` (um módulo por perfil de usuário), com a infraestrutura de UI em `src/app/` e uma biblioteca interna em `src/shared/`. As telas foram desenhadas no Figma com base no Material UI.
- **Backend:** API assíncrona em FastAPI, organizada em `routes` → `services` → `models`, com validação via Pydantic, documentação automática (Swagger/OpenAPI), rate limiting e recuperação de senha por e-mail. As trilhas adaptativas são geradas com o **Google Gemini**, e os arquivos enviados ficam no **AWS S3**.
- **CI/CD:** GitHub Actions para lint e testes (`ci.yml`) e deploy (`deploy.yml`).
- **Infraestrutura (AWS):**
  - uma instância EC2 `t3.medium` com os containers Docker do backend e do PostgreSQL;
  - um bucket S3 com o frontend estático;
  - o CloudFront como CDN, com HTTPS.

  O custo estimado é de cerca de US$ 32 por mês.

## Como rodar

**Frontend** (requer Node.js):

```sh
cd frontend
npm install
npm run dev        # http://localhost:5173
npm test           # testes unitários (Jest)
npm run test:e2e   # testes E2E (Playwright)
```

**Backend** (requer Docker):

```sh
cd backend
cp .env-example .env   # preencha as variáveis
docker compose up --build
```

Os READMEs de [`frontend/`](frontend) e [`backend/`](backend) têm instruções detalhadas.

## Branches

A branch `main` tem o estado final de cada repositório. As demais branches originais foram mantidas com o nome da pasta como prefixo, por exemplo `frontend/develop` e `backend/dev`.

## Equipe

**Professora coordenadora:** Aline de Campos

| Nível | Integrantes |
|---|---|
| AGES I | Antonio Augusto Fell Dal Bem, Arthur de Oliveira Ferreira, Douglas Lisboa Silvano, Isabella Martins Gernster, Lorenzo Santos de Souza de Moraes Bueno |
| AGES II | Felipe Prunes Rambor, Maria Eduarda Souza Melloni |
| AGES III | Adrielle Dornelles Dewes, Guilherme Melos Vieira, Gustavo Caldeira da Mesquita, Murilo Machado da Silva, Nicolas Fonseca Docolas |
| AGES IV | Ana Luiza Fraga Romanini, Lara Alves Kunrath Padilha, Léo Falcao Vieira Furtado, Maurício Pessoa de Mello Gaspary |

---

Repositórios originais: [tools.ages.pucrs.br/mapa-digital](https://tools.ages.pucrs.br/mapa-digital)
