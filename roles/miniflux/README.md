# Miniflux

## Alterando configurações padrão
As configurações padrão para novos usuários estão armazenados na tabela `users` do banco de dados, infelizmente não podem ser alteradas com uma linha de configuração ou variável de ambiente. As alterações só serão refletidas em novos usuários.

Primeiro, acesse o container do banco de dados e logue com o comando `psql`:
```bash
docker-compose exec db sh
psql -U $POSTGRES_USER -d $POSTGRES_DB
```

Altere a linguagem padrão:
```bash 
ALTER TABLE ONLY users ALTER COLUMN language SET DEFAULT 'pt_BR';
```

Altere o fuso horário padrão:
```bash
ALTER TABLE ONLY users ALTER COLUMN timezone SET DEFAULT 'America/Sao_Paulo';
```
