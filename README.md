
---

## 🔧 Alterações Realizadas no ED-010

Durante a execução do **Estudo Dirigido ED-010**, o backend do projeto **PATRI-TECH** passou por uma refatoração arquitetural com o objetivo de evoluir de uma API apenas funcional para uma API **coerente, previsível e alinhada a boas práticas profissionais**.

### Substituição de ViewSets por Views com Generics

Inicialmente, o projeto utilizava `ModelViewSet` em conjunto com `DefaultRouter`, o que gerava comportamentos implícitos e menor previsibilidade arquitetural.
Esse padrão foi substituído pelo uso exclusivo de **class-based views com `generics`**, adotando exatamente duas views por entidade:

* `<Entidade>ListCreateView`
* `<Entidade>DetailView`

Essa mudança torna o comportamento da API explícito, previsível e facilmente auditável.

---

### Padronização total entre as entidades

Todas as entidades do sistema (**Categoria, Status, Unidade, Sala e Bem**) passaram a seguir rigorosamente o mesmo padrão de implementação:

* Mesma estrutura de views
* Mesmas regras de permissão
* Mesmo formato de URLs
* Mesmo padrão de documentação no Swagger

Essa padronização elimina exceções silenciosas e facilita manutenção, testes e evolução do projeto.

---

### URLs explícitas e estáveis

As rotas da API deixaram de ser geradas automaticamente e passaram a ser declaradas manualmente, seguindo o padrão:

```text
/api/<entidade_plural>/
/api/<entidade_plural>/<id>/
```

Isso garante estabilidade para integração com front-end, clareza na documentação e previsibilidade no consumo da API.

---

### Regras de permissão unificadas

Foi adotada uma única regra de permissão para todas as entidades:

* `GET` → permitido sem autenticação
* `POST`, `PUT`, `PATCH` e `DELETE` → exigem autenticação

Essa decisão assegura consistência de segurança em toda a API e evita comportamentos divergentes entre endpoints.

---

### Documentação Swagger alinhada à implementação

A documentação foi ajustada para refletir fielmente o comportamento real da API, utilizando `@extend_schema(tags=[])`.
Todos os endpoints documentados no Swagger correspondem exatamente às rotas e permissões implementadas.

---

## ✅ Resultado

Ao final do ED-010, a API:

* deixa de ser apenas funcional
* passa a ser **coerente, previsível e padronizada**
* está pronta para:

  * implementação de filtros e ordenações
  * adição de regras de negócio
  * geração de relatórios
  * integração segura com front-end

Essas alterações alinham o projeto **PATRI-TECH** a práticas reais de engenharia de software, preparando o backend para crescimento sustentável e manutenção a longo prazo.

---

