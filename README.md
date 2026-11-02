# Git e GitHub para iniciantes

Um guia em português para quem está começando do zero. Você aprenderá a guardar o histórico de um projeto, compartilhá-lo e colaborar com outras pessoas. Não é preciso saber programar: Git também pode acompanhar documentos e arquivos de texto.

## Índice

1. [O que são Git e GitHub?](#o-que-são-git-e-github)
2. [Conceitos essenciais](#conceitos-essenciais)
3. [Preparação](#preparação)
4. [Seu primeiro repositório](#seu-primeiro-repositório)
5. [Publicando no GitHub](#publicando-no-github)
6. [Trabalhando em um projeto existente](#trabalhando-em-um-projeto-existente)
7. [Branches e colaboração](#branches-e-colaboração)
8. [Conflitos e cuidados](#conflitos-e-cuidados)
9. [Consulta rápida](#consulta-rápida)
10. [Exercício e próximos passos](#exercício-e-próximos-passos)

## O que são Git e GitHub?

**Git** é um programa de controle de versão: ele registra pontos da história dos arquivos de um projeto, permitindo consultar alterações e trabalhar em ideias diferentes. Ele funciona no computador, inclusive sem internet.

**GitHub** é uma plataforma na internet que hospeda repositórios Git e oferece recursos para compartilhar projetos, discutir tarefas e revisar contribuições. O Git não depende do GitHub; há outras plataformas semelhantes.

Imagine o Git como um álbum de versões do projeto e o GitHub como um lugar onde esse álbum pode ser compartilhado. Uma cópia online ajuda, mas não substitui uma estratégia de backup.

## Conceitos essenciais

| Termo | Significado |
| --- | --- |
| **Repositório** ou **repo** | Projeto acompanhado pelo Git, junto com seu histórico. |
| **Commit** | Registro de uma versão dos arquivos preparados, acompanhado de uma mensagem. |
| **Área de preparação** ou **staging** | Espaço onde você escolhe as alterações que entrarão no próximo commit. |
| **Branch** ou **ramificação** | Linha de trabalho para desenvolver uma ideia separadamente. A principal costuma se chamar `main`. |
| **Remoto** ou **remote** | Endereço de outra cópia do repositório, geralmente no GitHub. `origin` é um nome comum para esse endereço. |
| **Clone** | Cópia local de um repositório remoto, com seu histórico. |
| **Push** | Envia commits locais para um remoto. |
| **Pull** | Busca atualizações do remoto e tenta integrá-las à branch atual. |
| **Merge** | Integra alterações de uma linha de trabalho a outra. |
| **Pull request** ou **PR** | Pedido no GitHub para revisar e integrar alterações. |
| **Issue** | Espaço para registrar e discutir uma tarefa, dúvida ou problema. |

O fluxo mais comum é: **editar arquivos → preparar alterações → criar um commit → enviar ao GitHub**. Salvar um arquivo não cria um commit automaticamente; criar um commit também não o envia automaticamente ao GitHub.

## Preparação

1. Crie uma conta em [github.com](https://github.com/), caso ainda não tenha uma.
2. Instale o Git pelo [site oficial](https://git-scm.com/install/).
3. Abra um terminal: no Windows, você pode usar o Git Bash; no macOS ou Linux, o Terminal.
4. Confira a instalação com `git --version`. Se aparecer uma versão, o Git está disponível nesse terminal. Se o comando não for encontrado, confira a instalação e reabra o terminal.
5. Configure o nome e o e-mail que aparecerão nos seus commits, substituindo os exemplos:

   ```bash
   git config --global user.name "Seu Nome"
   git config --global user.email "voce@exemplo.com"
   ```

Para associar commits à conta do GitHub, use um e-mail cadastrado nela. Você também pode usar o endereço privado `noreply` fornecido pelo GitHub. A opção `--global` aplica a configuração aos repositórios do usuário no computador.

> O terminal executa comandos de texto. Pressione **Enter** depois de cada linha. Linhas iniciadas com `#` nos exemplos são comentários explicativos e não precisam ser digitadas.

## Seu primeiro repositório

Escolha um lugar para praticar e execute:

```bash
mkdir meu-primeiro-projeto
cd meu-primeiro-projeto
git init -b main
```

`mkdir` cria a pasta, `cd` entra nela e `git init` inicia o histórico do Git. Se sua versão não aceitar `-b`, atualize o Git ou consulte a documentação da sua versão.

Crie um arquivo chamado `anotacoes.txt` nessa pasta usando um editor de texto. Escreva algo, salve e volte ao terminal:

```bash
git status
git add anotacoes.txt
git status
git commit -m "Adiciona primeiras anotações"
```

- `git status` mostra o estado do trabalho e orientações sobre o que fazer.
- `git add` coloca a versão atual do arquivo na área de preparação. Se editá-lo novamente antes do commit, use `git add` outra vez para incluir as novas alterações.
- `git commit` registra os arquivos preparados. A mensagem deve explicar o que mudou.

Confira o histórico e as diferenças ainda não preparadas:

```bash
git log --oneline
git diff
```

Para ver as diferenças já preparadas para o próximo commit, use `git diff --staged`. Para preparar todos os arquivos novos e modificados da pasta atual e suas subpastas, existe `git add .`, mas confira `git status` antes para não incluir arquivos indesejados.

## Publicando no GitHub

Este exemplo parte do repositório local que você acabou de criar:

1. No GitHub, crie um novo repositório, por exemplo `meu-primeiro-projeto`. Escolha se ele será público ou privado. Para seguir estes passos, **não** inicialize o repositório online com README, licença ou `.gitignore`: isso evita criar um histórico separado.
2. Copie o endereço HTTPS exibido pelo GitHub e substitua o endereço de exemplo abaixo pelo seu:

   ```bash
   git remote add origin https://github.com/SEU-USUARIO/meu-primeiro-projeto.git
   git remote -v
   git push -u origin main
   ```

3. Atualize a página do repositório no navegador. Seu arquivo e o commit devem aparecer.

`remote add` associa o endereço ao nome `origin`. `push -u` envia a branch `main` e configura seu acompanhamento; depois disso, geralmente basta usar `git push` nessa branch. O GitHub pode pedir autenticação pelo navegador ou por um gerenciador de credenciais. A senha da conta não é usada como senha Git em operações por HTTPS; siga as instruções apresentadas. Nunca compartilhe tokens ou senhas.

Em um repositório **público**, qualquer pessoa pode ver o conteúdo. Em um **privado**, o acesso é restrito às pessoas autorizadas.

## Trabalhando em um projeto existente

Para obter uma cópia de um repositório que já existe, copie seu endereço no GitHub e execute, fora de outro repositório:

```bash
git clone https://github.com/USUARIO/NOME-DO-REPOSITORIO.git
cd NOME-DO-REPOSITORIO
git status
```

Antes de começar uma nova alteração em uma branch compartilhada, confira se não há trabalho local pendente com `git status` e atualize-a, quando apropriado, com `git pull`.

Depois de editar e salvar seus arquivos, o ciclo é `git status`, `git add`, `git commit` e `git push`. Você precisa de permissão de escrita para enviar diretamente ao repositório; sem ela, pode contribuir por meio de um **fork**, explicado abaixo.

## Branches e colaboração

Uma branch permite trabalhar em uma ideia sem alterar imediatamente a branch principal. Por exemplo, em uma cópia atualizada do projeto:

```bash
git switch -c adiciona-exemplo
# Edite e salve os arquivos.
git status
git add anotacoes.txt
git commit -m "Adiciona exemplo ao guia"
git push -u origin adiciona-exemplo
```

No GitHub, abra um **pull request** da branch `adiciona-exemplo` para `main`, explique o que mudou e peça revisão quando fizer sentido. Após a revisão, uma pessoa com permissão pode integrar o PR. Para voltar à branch principal e atualizá-la localmente depois da integração:

```bash
git switch main
git pull
```

Em projetos de outras pessoas, talvez seja necessário criar um **fork** pelo botão correspondente no GitHub: ele cria uma cópia do repositório na sua conta. Clone seu fork, crie uma branch, envie suas alterações para ele e abra um PR do seu fork para o projeto original. Leia as instruções de contribuição do projeto antes de enviar.

## Conflitos e cuidados

Um **conflito** pode ocorrer quando o Git não consegue decidir sozinho como combinar alterações, por exemplo, quando duas pessoas mudam a mesma linha. Leia as mensagens do terminal e siga estas etapas gerais:

1. Execute `git status` para identificar os arquivos em conflito.
2. Abra cada arquivo, procure os marcadores `<<<<<<<`, `=======` e `>>>>>>>`, decida qual conteúdo deve ficar e remova os marcadores.
3. Salve, revise o resultado e use `git add` nos arquivos resolvidos.
4. Conclua a operação conforme a orientação de `git status`. Em um merge, normalmente será necessário `git commit`; em um rebase, use `git rebase --continue`.

Se não souber qual conteúdo manter, peça ajuda antes de concluir.

**Nunca envie senhas, chaves de API, tokens ou dados pessoais ao repositório.** Um arquivo `.gitignore` pode impedir que arquivos ainda não rastreados sejam adicionados por acidente, mas não remove arquivos que o Git já acompanha nem apaga segredos do histórico. Se um segredo for publicado, revogue ou substitua-o imediatamente e siga as orientações do serviço afetado.

## Consulta rápida

| Comando | Para que serve |
| --- | --- |
| `git status` | Ver o estado dos arquivos e da operação atual. |
| `git add arquivo.txt` | Preparar a versão atual de um arquivo. |
| `git commit -m "mensagem"` | Registrar as alterações preparadas. |
| `git log --oneline` | Consultar o histórico resumido. |
| `git diff` / `git diff --staged` | Ver alterações não preparadas / preparadas. |
| `git branch` | Listar branches locais e indicar a atual. |
| `git switch -c nome` | Criar uma branch e mudar para ela. |
| `git switch main` | Mudar para a branch `main`, se existir. |
| `git pull` | Buscar e integrar atualizações da branch acompanhada. |
| `git push` | Enviar commits da branch atual ao remoto configurado. |
| `git clone URL` | Copiar um repositório remoto para uma nova pasta. |

Se um comando falhar, leia a mensagem e execute `git status` antes de tentar outro. Evite copiar comandos destrutivos sem entender o que fazem.

## Exercício e próximos passos

1. Crie um repositório de prática e faça um primeiro commit com um arquivo de apresentação.
2. Edite o arquivo, confira a diferença com `git diff` e faça outro commit.
3. Crie um repositório vazio no GitHub e envie seus commits.
4. Crie uma branch, acrescente uma informação e abra um pull request.
5. Depois de integrar o PR, atualize sua cópia local e examine o histórico.

Para continuar aprendendo, consulte a [documentação oficial do Git](https://git-scm.com/doc) e a [documentação do GitHub](https://docs.github.com/pt). O [GitHub Skills](https://skills.github.com/) oferece exercícios interativos.
