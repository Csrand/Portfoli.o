# 🛠️ Sistema de Ordem de Serviço + Calendário Colaborativo


## 📖 Sobre o Projeto

Sistema web desenvolvido para centralizar o acompanhamento de ordens de serviço e eventos corporativos. Focado em melhorar a comunicação interna e reduzir retrabalho em equipes de manutenção aeronáutica.

### ✨ Funcionalidades Principais

- 📋 **Ordens de Serviço** - Criação, acompanhamento e histórico completo de status
- 📅 **Calendário Colaborativo** - Eventos visuais tipo "post-it" para toda a equipe
- 📊 **Dashboard com KPIs** - Métricas de desempenho da equipe (semana/mês/ano)
- 📸 **Upload de Fotos** - Integração com Cloudinary para documentação visual
- 🔐 **Autenticação JWT** - Login seguro com perfis de acesso diferenciados
- 📱 **Mobile First** - Totalmente responsivo para acesso em qualquer dispositivo

---

## 🚀 Tecnologias Utilizadas

### Front-end
| Tecnologia | Versão | Propósito |
|------------|--------|-----------|
| React | 18.x | Interface de usuário |
| TypeScript | 5.x | Tipagem estática |
| Vite | 5.x | Build tool |
| Tailwind CSS | 3.x | Estilização |
| React Router | 6.x | Navegação |
| Axios | 1.x | Cliente HTTP |
| Vitest | 1.x | Testes unitários |

### Back-end
| Tecnologia | Versão | Propósito |
|------------|--------|-----------|
| Node.js | 20.x | Runtime |
| Express | 4.x | Framework web |
| TypeScript | 5.x | Tipagem estática |
| PostgreSQL | 15.x | Banco de dados |
| Prisma/TypeORM | - | ORM |
| JWT | - | Autenticação |
| bcrypt | - | Hash de senhas |
| Cloudinary | - | Storage de imagens |

### Infraestrutura
| Serviço | Propósito |
|---------|-----------|
| Vercel | Deploy front-end |
| Railway | Deploy back-end + banco |
| Cloudinary | Armazenamento de fotos |
| GitHub Actions | CI/CD |

---

## 📋 Requisitos

- Node.js 20.x ou superior
- npm ou yarn
- PostgreSQL 15.x (local ou Railway)
- Conta no Cloudinary (free tier)
- Conta na Vercel (free tier)
- Conta na Railway (free tier)

---

## 🔧 Instalação e Setup

### 1. Clone o Repositório

```bash
git clone https://github.com/seuusuario/service-order-system.git
cd service-order-system
```

### 2. Setup do Back-end

```bash
# Navegue para pasta do back-end
cd backend

# Instale dependências
npm install

# Copie arquivo de exemplo de variáveis de ambiente
cp .env.example .env

# Edite .env com suas credenciais
# DATABASE_URL=postgresql://...
# JWT_SECRET=sua_chave_secreta
# CLOUDINARY_CLOUD_NAME=...
# CLOUDINARY_API_KEY=...
# CLOUDINARY_API_SECRET=...

# Execute migrations do banco
npm run migrate

# Inicie o servidor em desenvolvimento
npm run dev
```

**Back-end rodará em:** `http://localhost:3333`

### 3. Setup do Front-end

```bash
# Navegue para pasta do front-end (nova aba do terminal)
cd frontend

# Instale dependências
npm install

# Copie arquivo de exemplo de variáveis de ambiente
cp .env.example .env

# Edite .env com a URL da API
# VITE_API_URL=http://localhost:3333

# Inicie o servidor de desenvolvimento
npm run dev
```

**Front-end rodará em:** `http://localhost:5173`

---

## 📁 Estrutura do Projeto

```
service-order-system/
├── backend/
│   ├── src/
│   │   ├── modules/
│   │   │   ├── service-orders/
│   │   │   │   ├── controllers/
│   │   │   │   ├── services/
│   │   │   │   ├── repositories/
│   │   │   │   ├── dtos/
│   │   │   │   └── entities/
│   │   │   └── calendar/
│   │   │       ├── controllers/
│   │   │       ├── services/
│   │   │       ├── repositories/
│   │   │       ├── dtos/
│   │   │       └── entities/
│   │   ├── shared/
│   │   │   ├── middlewares/
│   │   │   ├── errors/
│   │   │   ├── utils/
│   │   │   └── database/
│   │   ├── config/
│   │   └── app.ts
│   ├── prisma/
│   ├── tests/
│   ├── .env.example
│   ├── package.json
│   └── tsconfig.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── atoms/
│   │   │   ├── molecules/
│   │   │   ├── organisms/
│   │   │   └── templates/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── contexts/
│   │   ├── types/
│   │   ├── utils/
│   │   └── App.tsx
│   ├── public/
│   ├── .env.example
│   ├── package.json
│   ├── tailwind.config.js
│   └── vite.config.ts
├── .gitignore
├── README.md
└── docs/
    └── API.md
```

---

## 🔌 API Endpoints

### Autenticação

| Método | Endpoint | Descrição | Auth |
|--------|----------|-----------|------|
| POST | `/api/auth/register` | Criar nova conta | ❌ |
| POST | `/api/auth/login` | Fazer login | ❌ |
| POST | `/api/auth/refresh` | Renovar token | ✅ |

### Ordens de Serviço

| Método | Endpoint | Descrição | Auth |
|--------|----------|-----------|------|
| GET | `/api/orders` | Listar todas ordens | ✅ |
| GET | `/api/orders/:id` | Buscar ordem por ID | ✅ |
| POST | `/api/orders` | Criar nova ordem | ✅ (Admin) |
| PUT | `/api/orders/:id` | Atualizar ordem | ✅ (Admin) |
| PUT | `/api/orders/:id/status` | Atualizar status | ✅ (Admin) |
| POST | `/api/orders/:id/photos` | Upload de fotos | ✅ (Admin) |
| GET | `/api/orders/:id/history` | Histórico de status | ✅ |

### Calendário

| Método | Endpoint | Descrição | Auth |
|--------|----------|-----------|------|
| GET | `/api/events` | Listar eventos | ✅ |
| POST | `/api/events` | Criar evento | ✅ (Admin) |
| PUT | `/api/events/:id` | Atualizar evento | ✅ (Admin) |
| DELETE | `/api/events/:id` | Deletar evento | ✅ (Admin) |

### Dashboard

| Método | Endpoint | Descrição | Auth |
|--------|----------|-----------|------|
| GET | `/api/dashboard/kpis` | KPIs da equipe | ✅ |
| GET | `/api/dashboard/ranking` | Ranking de técnicos | ✅ |

---

## 🧪 Testes

### Back-end

```bash
cd backend

# Rodar todos testes
npm test

# Rodar com coverage
npm run test:coverage

# Rodar em watch mode
npm run test:watch
```

### Front-end

```bash
cd frontend

# Rodar todos testes
npm test

# Rodar com coverage
npm run test:coverage
```

**Meta de Coverage:** 70% mínimo

---

## 🚀 Deploy

### Front-end (Vercel)

1. Crie conta em [vercel.com](https://vercel.com)
2. Conecte seu repositório GitHub
3. Configure variáveis de ambiente:
   - `VITE_API_URL` = URL do back-end em produção
4. Deploy automático em cada push na main

### Back-end (Railway)

1. Crie conta em [railway.app](https://railway.app)
2. Crie novo projeto → Deploy from GitHub
3. Configure variáveis de ambiente:
   - `DATABASE_URL`
   - `JWT_SECRET`
   - `CLOUDINARY_*`
4. Railway provisiona PostgreSQL automaticamente

### Banco de Dados

- Migrations rodam automaticamente no deploy
- Backup diário automático (Railway)
- SSL ativo por padrão

---

## 👥 Perfis de Usuário

| Perfil | Permissões |
|--------|------------|
| **Administrativo** | Criar/editar ordens, criar eventos, ver KPIs |
| **Técnico** | Visualizar ordens, visualizar calendário (somente leitura) |
| **Visualizador** | Visualizar ordens, visualizar calendário (somente leitura) |

---

## 📊 Modelo de Dados

```
Usuario (1) ──< OrdemServico (N)
Usuario (1) ──< Evento (N)
OrdemServico (1) ──< FotoOrdem (N)
OrdemServico (1) ──< HistoricoStatus (N)
```

**Principais Entidades:**

- `Usuario`: id, nome, email, senha_hash, cargo, criado_em
- `OrdemServico`: id, cliente, descricao, prioridade, status, data_limite, responsavel_id, criado_por, criado_em
- `Evento`: id, titulo, descricao, data_inicio, data_fim, tipo, criado_por, criado_em
- `FotoOrdem`: id, ordem_id, url, cloudinary_id, criado_em
- `HistoricoStatus`: id, ordem_id, status, mudanca_por, mudanca_em

---

## 🎯 Roadmap

### ✅ MVP (Fase 1) - 4 semanas
- [x] Autenticação JWT
- [x] CRUD Ordens de Serviço
- [x] Calendário colaborativo
- [x] Dashboard com KPIs
- [x] Upload de fotos
- [x] Deploy em produção

### 🔜 Fase 2 (Próximos Passos)
- [ ] Perfil Administrador (CRUD usuários)
- [ ] Notificações por email
- [ ] Integração Google Calendar
- [ ] Relatórios em PDF
- [ ] WebSocket para tempo real

### 💡 Futuro
- [ ] Aplicativo mobile nativo
- [ ] API pública para integrações
- [ ] Multi-tenant (múltiplas empresas)

---

## 📝 Decisões Técnicas (ADRs)

### ADR-001: Cloudinary vs AWS S3
**Decisão:** Cloudinary  
**Motivo:** Free tier generoso, mais simples de implementar, transformações de imagem automáticas

### ADR-002: JWT vs Session
**Decisão:** JWT  
**Motivo:** Padrão de mercado, stateless, fácil de escalar

### ADR-003: PostgreSQL vs MongoDB
**Decisão:** PostgreSQL  
**Motivo:** Dados relacionais, experiência prévia da equipe, integridade referencial

### ADR-004: Mobile First
**Decisão:** Desenvolver para mobile primeiro  
**Motivo:** Técnicos acessam em campo, mercado exige responsividade

---

## 🐛 Bugs Conhecidos

| ID | Descrição | Status | Prioridade |
|----|-----------|--------|------------|
| - | Nenhum no momento | - | - |

Reporte bugs abrindo uma [issue](https://github.com/seuusuario/service-order-system/issues).

---

## 🤝 Como Contribuir

1. Fork o projeto
2. Crie branch para feature (`git checkout -b feature/nova-feature`)
3. Commit mudanças (`git commit -m 'feat: adiciona nova feature'`)
4. Push para branch (`git push origin feature/nova-feature`)
5. Abra Pull Request

**Padrão de Commits:**
- `feat:` nova funcionalidade
- `fix:` correção de bug
- `docs:` documentação
- `style:` formatação
- `refactor:` refatoração
- `test:` testes
- `chore:` configurações

---

## 📄 Licença

MIT License - veja [LICENSE](LICENSE) para detalhes.

---

## 📞 Contato

**Desenvolvedor Responsável:** [Seu Nome]  
**Email:** [seu.email@email.com]  
**LinkedIn:** [linkedin.com/in/seu-perfil]  
**Repositório:** [github.com/seuusuario/service-order-system](https://github.com/seuusuario/service-order-system)

---

## 🙏 Agradecimentos

- D.A Aviação pelo desafio e confiança
- Comunidade open-source pelas ferramentas utilizadas
- Mentores e colegas pelo apoio no desenvolvimento
