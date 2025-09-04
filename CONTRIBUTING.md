# 🤝 Contribuindo para o NFGuard

Obrigado por considerar contribuir para o NFGuard! Este documento fornece diretrizes para contribuições ao projeto.

## 📋 Índice

- [Como Contribuir](#como-contribuir)
- [Reportando Bugs](#reportando-bugs)
- [Sugerindo Melhorias](#sugerindo-melhorias)
- [Desenvolvimento](#desenvolvimento)
- [Padrões de Código](#padrões-de-código)
- [Processo de Pull Request](#processo-de-pull-request)
- [Documentação](#documentação)
- [Comunidade](#comunidade)

## 🚀 Como Contribuir

Existem várias maneiras de contribuir para o NFGuard:

- 🐛 Reportar bugs
- 💡 Sugerir novas funcionalidades
- 📝 Melhorar a documentação
- 🔧 Corrigir problemas existentes
- 🌐 Traduzir conteúdo
- 🧪 Escrever testes

## 🐛 Reportando Bugs

Antes de reportar um bug, verifique se ele já não foi reportado nas [Issues](https://github.com/nfguard/nfguard/issues).

### Como reportar um bug:

1. Use um título claro e descritivo
2. Descreva os passos para reproduzir o problema
3. Explique o comportamento esperado vs. o comportamento atual
4. Inclua informações do sistema:
   - Versão do NFGuard
   - Sistema operacional
   - Versão do kernel
   - Distribuição Linux

### Template para Bug Report:

```markdown
**Descrição do Bug**
Uma descrição clara e concisa do bug.

**Passos para Reproduzir**
1. Vá para '...'
2. Execute '...'
3. Veja o erro

**Comportamento Esperado**
O que deveria acontecer.

**Screenshots/Logs**
Se aplicável, adicione screenshots ou logs.

**Ambiente:**
 - OS: [ex: Ubuntu 22.04]
 - Kernel: [ex: 5.15.0]
 - NFGuard Version: [ex: 1.0.0]
```

## 💡 Sugerindo Melhorias

Sugestões de melhorias são sempre bem-vindas! Para sugerir uma melhoria:

1. Verifique se a sugestão já não existe nas Issues
2. Abra uma nova Issue com o label "enhancement"
3. Descreva detalhadamente a melhoria proposta
4. Explique por que seria útil para o projeto

## 🔧 Desenvolvimento

### Pré-requisitos

- Linux (Ubuntu 20.04+ recomendado)
- NFTables instalado
- Python 3.8+
- Git

### Configuração do Ambiente

```bash
# Clone o repositório
git clone https://github.com/nfguard/nfguard.git
cd nfguard

# Instale as dependências
sudo apt update
sudo apt install nftables python3-pip
pip3 install -r requirements.txt

# Configure o ambiente de desenvolvimento
cp config/nfguard.yml.example config/nfguard.yml
```

### Estrutura do Projeto

```
nfguard/
├── src/                 # Código fonte principal
├── config/              # Arquivos de configuração
├── rules/               # Regras YAML
├── tests/               # Testes automatizados
├── docs/                # Documentação
├── scripts/             # Scripts auxiliares
└── examples/            # Exemplos de uso
```

## 📏 Padrões de Código

### Python

- Siga o [PEP 8](https://pep8.org/)
- Use type hints quando possível
- Docstrings para funções e classes
- Máximo de 88 caracteres por linha

### YAML

- Use 2 espaços para indentação
- Nomes de chaves em snake_case
- Comentários explicativos quando necessário

### Commits

Use o padrão [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: adiciona suporte para IPv6
fix: corrige parsing de regras YAML
docs: atualiza README com exemplos
test: adiciona testes para módulo de firewall
```

### Tipos de commit:

- `feat`: nova funcionalidade
- `fix`: correção de bug
- `docs`: documentação
- `style`: formatação de código
- `refactor`: refatoração
- `test`: testes
- `chore`: tarefas de manutenção

## 🔄 Processo de Pull Request

1. **Fork** o repositório
2. **Clone** seu fork localmente
3. **Crie** uma branch para sua feature:
   ```bash
   git checkout -b feature/nova-funcionalidade
   ```
4. **Faça** suas alterações seguindo os padrões
5. **Teste** suas alterações:
   ```bash
   python -m pytest tests/
   ```
6. **Commit** suas alterações:
   ```bash
   git commit -m "feat: adiciona nova funcionalidade"
   ```
7. **Push** para seu fork:
   ```bash
   git push origin feature/nova-funcionalidade
   ```
8. **Abra** um Pull Request

### Checklist do Pull Request

- [ ] Código segue os padrões estabelecidos
- [ ] Testes passam localmente
- [ ] Documentação foi atualizada (se necessário)
- [ ] Commit messages seguem o padrão
- [ ] PR tem descrição clara do que foi alterado
- [ ] Não quebra funcionalidades existentes

### Template do Pull Request

```markdown
## Descrição
Descreva brevemente as alterações realizadas.

## Tipo de Mudança
- [ ] Bug fix
- [ ] Nova funcionalidade
- [ ] Breaking change
- [ ] Documentação

## Como Testar
1. Passo 1
2. Passo 2
3. Passo 3

## Checklist
- [ ] Meu código segue os padrões do projeto
- [ ] Realizei uma auto-revisão do código
- [ ] Comentei partes complexas do código
- [ ] Atualizei a documentação
- [ ] Meus commits seguem o padrão estabelecido
- [ ] Adicionei testes que provam que minha correção/funcionalidade funciona
- [ ] Testes novos e existentes passam localmente
```

## 📚 Documentação

A documentação é mantida em:

- **README.md**: Informações gerais e instalação
- **docs/**: Documentação técnica detalhada
- **examples/**: Exemplos práticos de uso
- **Banco de Memória/**: Documentação interna do projeto

### Atualizando Documentação

- Mantenha a documentação atualizada com as mudanças
- Use linguagem clara e exemplos práticos
- Inclua capturas de tela quando apropriado
- Documente APIs e configurações

## 🌐 Tradução

O NFGuard suporta múltiplos idiomas. Para contribuir com traduções:

1. Verifique os arquivos em `languages/`
2. Adicione ou atualize traduções
3. Teste em ambos os idiomas
4. Mantenha consistência entre traduções

## 🧪 Testes

### Executando Testes

```bash
# Todos os testes
python -m pytest

# Testes específicos
python -m pytest tests/test_firewall.py

# Com cobertura
python -m pytest --cov=src
```

### Escrevendo Testes

- Use pytest como framework
- Teste casos de sucesso e falha
- Mock dependências externas
- Mantenha testes isolados e determinísticos

## 🏷️ Versionamento

O NFGuard segue [Semantic Versioning](https://semver.org/):

- **MAJOR**: Mudanças incompatíveis
- **MINOR**: Novas funcionalidades compatíveis
- **PATCH**: Correções de bugs

## 🤝 Comunidade

### Código de Conduta

- Seja respeitoso e inclusivo
- Aceite críticas construtivas
- Foque no que é melhor para a comunidade
- Mostre empatia com outros membros

### Canais de Comunicação

- **Issues**: Para bugs e sugestões
- **Discussions**: Para perguntas gerais
- **Email**: contato@nfguard.org

### Reconhecimento

Todos os contribuidores são reconhecidos no arquivo CONTRIBUTORS.md e nos releases do projeto.

## 📄 Licença

Ao contribuir, você concorda que suas contribuições serão licenciadas sob a mesma licença do projeto.

## ❓ Dúvidas

Se tiver dúvidas sobre como contribuir:

1. Verifique a documentação existente
2. Procure em Issues fechadas
3. Abra uma Discussion
4. Entre em contato: lucas@dolutech.com

---

**Obrigado por contribuir para o NFGuard! 🚀**

Juntos, estamos construindo uma alternativa moderna e eficiente para o gerenciamento de firewall no Linux.
