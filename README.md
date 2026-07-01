# Documentação de Integração IplanRio

Este repositório contém a documentação técnica completa da infraestrutura de integração da IplanRio. A documentação abrange todos os aspectos da integração de sistemas, desde o Data Lake até as APIs e serviços de autenticação.

## Estrutura da Documentação 

A documentação está organizada nas seguintes seções principais:

- **Introdução**: Documentos introdutórios e guias rápidos
- **Data Lake**: 
  - Guias de desenvolvimento
  - Tipos de pipeline
  - Guias de estilo para dados
  - Processos de ETL
- **Barramento de Dados**: 
  - Referências de API
  - Documentação de endpoints
  - Guias de integração
- **MCP (Message Control Platform)**:
  - Arquitetura
  - Configuração
  - Fluxos de mensageria
- **Autenticação e Segurança**:
  - Protocolos de autenticação
  - Gerenciamento de tokens
  - Políticas de segurança

## Desenvolvimento Local

### Opção 1: Usando Nix (Recomendado)

Este projeto usa Nix para garantir um ambiente de desenvolvimento reproduzível com todas as dependências corretas.

1. Instale Nix se ainda não tiver:
```bash
curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix | sh -s -- install
```

2. Entre no ambiente de desenvolvimento:
```bash
nix develop
```

3. Inicie o servidor de desenvolvimento:
```bash
mintlify dev
```

Ou use o script de conveniência:
```bash
./start-dev.sh
```

O servidor iniciará em `http://localhost:3000`

### Opção 2: Usando npm diretamente

Se preferir não usar Nix, você pode instalar Mintlify globalmente:

1. Certifique-se de ter Node.js 20+ instalado
2. Instale o [Mintlify CLI](https://www.npmjs.com/package/mintlify):
```bash
npm i -g mintlify
```

3. Execute o servidor de desenvolvimento:
```bash
mintlify dev
```

## Publicação de Alterações

As alterações são publicadas automaticamente através do GitHub App do Mintlify. Ao fazer push para a branch principal, as mudanças serão automaticamente implantadas em produção.

## Solução de Problemas

- Se o `mintlify dev` não estiver funcionando, execute `mintlify install` para reinstalar as dependências
- Se a página carregar como 404, verifique se você está executando o comando em uma pasta que contém o arquivo `docs.json`

## Links Úteis

- [Site IplanRio](https://www.iplan.rio/)
- [Discord IplanRio](https://discord.gg/myFqCKr3)
- [Dashboard Mintlify](https://dashboard.mintlify.com)

## Contribuindo

Para contribuir com a documentação:

1. Crie uma branch para sua contribuição
2. Faça suas alterações seguindo o guia de estilo da documentação
3. Envie um Pull Request para revisão
4. Após aprovado, suas alterações serão publicadas automaticamente

## Suporte

Para suporte técnico, entre em contato através do email: hi@mintlify.com
