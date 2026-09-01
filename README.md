# SistemaCadastro

Projeto desenvolvido para a **Atividade Prática – Controle de Versão e Gerenciamento de Mudanças com Git**
da disciplina *Manutenção e Configuração de Software* (Aula 4).

O sistema é um pequeno programa Java que apresenta um menu no console. As funcionalidades
não são implementadas: o objetivo da atividade é trabalhar o **versionamento** do projeto.

## Estrutura

```
SistemaCadastro/
├── src/
│   └── SistemaCadastro.java
├── .gitignore
└── README.md
```

## Como compilar e executar

```bash
javac -encoding UTF-8 -d bin src/SistemaCadastro.java
java -cp bin SistemaCadastro
```

Saída esperada (após o merge da branch `feature/cadastro`):

```
=== Sistema de Cadastro ===
1 - Cadastrar usuário
2 - Listar usuários
3 - Excluir usuário
0 - Sair
```

## Histórico de versões

| Versão | Descrição |
|--------|-----------|
| inicial | Menu com as opções 1, 2 e 0 |
| v1.1.0 | Adicionada a opção `3 - Excluir usuário` (branch `feature/cadastro`) |

---

# Análise rápida

### 1. Qual a finalidade de uma branch?

Uma **branch** (ramificação) é uma linha de desenvolvimento paralela à versão principal do
projeto. Sua finalidade é permitir que novas funcionalidades sejam desenvolvidas, que erros
sejam corrigidos e que mudanças sejam testadas **sem afetar a versão principal** do sistema.

Enquanto o trabalho está em uma branch, a `main` permanece estável e funcional. Somente
depois que o desenvolvimento é concluído e revisado é que as alterações são integradas à
versão principal. Isso também permite que vários desenvolvedores trabalhem ao mesmo tempo,
cada um em sua própria branch, sem interferir no trabalho dos demais.

Nesta atividade, a branch `feature/cadastro` foi usada para desenvolver a opção
`3 - Excluir usuário` isoladamente, antes de integrá-la à `main`.

### 2. Qual a diferença entre commit e merge?

- **Commit**: é o registro de **uma alteração** feita no projeto. Cada commit guarda os
  arquivos modificados, uma mensagem descritiva, o autor e a data da mudança. O commit
  acontece **dentro de uma única branch** e é o que forma o histórico de evolução do sistema.

- **Merge**: é o processo de **integrar** as alterações de uma branch em outra. O merge não
  cria uma alteração nova de conteúdo — ele combina trabalhos que foram desenvolvidos
  separadamente, unindo dois históricos em um só.

Resumindo: o *commit* **registra** uma mudança em uma linha de desenvolvimento; o *merge*
**une** duas linhas de desenvolvimento diferentes. Vários commits são feitos em uma branch e,
ao final, um único merge leva todos eles para a branch principal.

### 3. Por que é importante utilizar mensagens claras nos commits?

Porque a mensagem é a única explicação do **motivo** da mudança — o código mostra *o que*
mudou, mas não *por quê*. Mensagens claras permitem:

- entender a evolução do sistema sem precisar ler todo o código;
- localizar rapidamente quando e onde um erro foi introduzido;
- facilitar a revisão de código e a comunicação dentro da equipe;
- gerar notas de versão (*changelog*) a partir do próprio histórico.

Padrões de prefixo, como os usados nesta atividade (`FIX[1]`, `FEAT[1]`), tornam o histórico
ainda mais organizado, pois classificam o tipo de cada mudança (correção, nova funcionalidade,
documentação etc.).

### 4. Por que o controle de versão é importante em equipes de desenvolvimento?

Porque em um projeto colaborativo várias pessoas alteram os mesmos arquivos ao mesmo tempo.
O controle de versão garante organização nesse cenário, permitindo:

- **rastrear modificações**: saber quem alterou o quê, quando e por quê;
- **recuperar versões anteriores**: voltar a um estado estável quando algo quebra;
- **trabalhar em paralelo**: cada pessoa em sua branch, sem sobrescrever o trabalho alheio;
- **evitar perda de código e resolver conflitos** de forma controlada;
- **apoiar a gerência de mudanças**: toda alteração fica analisada, aprovada e registrada.

Sem controle de versão, projetos grandes se tornam praticamente impossíveis de manter e evoluir.

### 5. O que representa a versão 1.1.0 no contexto desta atividade?

A versão segue o **versionamento semântico**, no formato `MAJOR.MINOR.PATCH`:

- **MAJOR (1)** – mudanças grandes, que quebram compatibilidade;
- **MINOR (1)** – novas funcionalidades compatíveis com a versão anterior;
- **PATCH (0)** – correções de erros.

Neste projeto, a versão inicial correspondia à `1.0.0`. Com a integração da branch
`feature/cadastro`, foi adicionada a **nova funcionalidade** `3 - Excluir usuário`, que não
quebra nada do que já existia. Por isso o número **MINOR** foi incrementado de `0` para `1`,
e o **PATCH** foi zerado, resultando em **`v1.1.0`**.

Ou seja: `v1.1.0` marca o ponto exato do histórico em que o sistema passou a contar com a
opção de exclusão de usuário.

### 6. Comandos Git para criar a tag pela interface CLI

A tag `v1.1.0` pode ser criada pela interface do GitHub (*Releases → Create a new release*),
mas o mesmo resultado é obtido pela linha de comando:

```bash
# 1. Garantir que está na branch principal, já com o merge realizado
git checkout main

# 2. Criar a tag anotada (recomendada: guarda autor, data e mensagem)
git tag -a v1.1.0 -m "Versão 1.1.0 - Adicionada opção de exclusão de usuário"

# 3. Enviar a tag para o GitHub
git push origin v1.1.0
```

Comandos auxiliares úteis:

```bash
git tag                  # lista todas as tags
git show v1.1.0          # exibe os detalhes da tag e do commit apontado
git push origin --tags   # envia todas as tags locais de uma vez
git tag -d v1.1.0                  # apaga a tag localmente
git push origin --delete v1.1.0    # apaga a tag no GitHub
```

> Observação: `git tag v1.1.0` (sem o `-a`) também funciona, mas cria uma *lightweight tag*,
> que é apenas um apelido para o commit, sem autor, data ou mensagem próprios. Para marcar
> versões de release, a tag anotada (`-a`) é a boa prática.

