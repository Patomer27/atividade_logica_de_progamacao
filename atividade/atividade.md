# Respostas da Atividade - Git e GitHub

### 1. Explique o conceito de controle de versão distribuído e descreva como o Git implementa esse modelo.

- **Conceito:** Em um sistema de controle de versão distribuído (DVCS), os desenvolvedores não dependem de um único servidor central para consultar o histórico do código. Cada membro da equipe possui uma cópia completa e local de todo o repositório — incluindo o histórico de alterações, ramificações (branches) e commits.
- **Implementação no Git:** O Git funciona de forma totalmente local. Quando você clona um projeto (`git clone`), ele baixa o histórico inteiro para a sua máquina. A sincronização com outros servidores (como o GitHub) só acontece quando você decide enviar (`git push`) ou puxar (`git pull`) alterações deliberadamente.

---

### 2. Diferencie Git e GitHub, destacando suas responsabilidades dentro do processo de desenvolvimento de software.

- **Git:** É a ferramenta de software de controle de versão que roda localmente na sua máquina. Ele é responsável por rastrear as mudanças nos arquivos, criar ramificações (branches), registrar históricos (commits) e gerenciar fusões (merges).
- **GitHub:** É uma plataforma de hospedagem baseada na nuvem que armazena os repositórios Git remotos. Ele adiciona uma interface visual e ferramentas colaborativas cruciais para o trabalho em equipe, como gerenciamento de acessos, Pull Requests, controle de problemas (Issues) e automações (CI/CD).

---

### 3. Explique o funcionamento interno de um commit no Git e sua importância para o histórico do projeto.

- **Funcionamento Interno:** Diferente de sistemas antigos que salvam apenas as diferenças de texto, o Git funciona tirando uma foto (_snapshot_) de como todos os arquivos do projeto estão naquele exato momento. Internamente, um commit é um objeto que contém uma referência a esse snapshot, metadados (autor, data, hora, mensagem explicativa) e um ponteiro para o commit anterior (o commit pai).
- **Importância:** O commit cria um ponto definitivo na linha do tempo. Ele permite rastrear a evolução do software, entender o porquê de cada mudança e reverter o código para um estado anterior seguro caso algo quebre.

---

### 4. Descreva o fluxo de trabalho do Git envolvendo Working Directory, Staging Area e Repository.

O ciclo de vida de uma alteração no Git passa por três estados principais:

1. **Working Directory (Diretório de Trabalho):** É a pasta local no seu computador onde você cria, edita e deleta os arquivos do projeto. Modificações aqui ainda não são rastreadas de forma definitiva pelo Git.
2. **Staging Area (Área de Preparação / Index):** Quando você roda o comando `git add`, os arquivos modificados saem do Working Directory e entram nesta área. Ela funciona como um "carrinho de compras" onde você seleciona e revisa exatamente o que deseja incluir na sua próxima foto do projeto.
3. **Repository (Repositório / diretório .git):** Quando você roda `git commit`, o Git pega tudo o que estava na Staging Area e grava permanentemente no banco de dados local, criando um novo registro oficial no histórico do projeto.

---

### 5. Explique o conceito de branch e discuta sua importância em ambientes colaborativos de desenvolvimento.

- **Conceito:** Uma branch (ramificação) no Git é simplesmente um ponteiro móvel e leve que aponta para um commit específico. Ela representa uma linha de desenvolvimento independente paralela à linha principal (`main`).
- **Importância Colaborativa:** Em equipes, as branches permitem que vários desenvolvedores trabalhem em funcionalidades (_features_) ou correções de bugs diferentes ao mesmo tempo, sem que o código de um interfira ou quebre o trabalho do outro. O código só é unificado quando está pronto e testado.

---

### 6. Diferencie os comandos merge e rebase, apresentando vantagens e desvantagens de cada abordagem.

- **Git Merge:** Une duas branches criando um novo "commit de merge" (_merge commit_) que junta os históricos.
  - _Vantagem:_ Preserva o histórico real, cronológico e fiel de como e quando as ramificações aconteceram.
  - _Desvantagem:_ O histórico pode ficar poluído e confuso visualmente (com muitos caminhos cruzados) em projetos grandes.
- **Git Rebase:** Pega os commits da sua branch atual e os reaplica ("reescreve") diretamente no topo de outra branch (geralmente a `main`).
  - _Vantagem:_ Cria um histórico perfeitamente linear, limpo e muito fácil de ler.
  - _Desvantagem:_ Reescreve o histórico do Git. Se usado incorretamente em branches públicas compartilhadas com outras pessoas, pode gerar sérios conflitos e confusões na equipe.

---

### 7. Explique o papel do arquivo .gitignore e descreva situações práticas onde sua utilização é indispensável.

- **Papel:** É um arquivo de texto localizado na raiz do projeto que dita ao Git quais arquivos ou pastas ele deve ignorar completamente, impedindo que sejam rastreados ou enviados acidentalmente para o repositório remoto.
- **Situações Práticas Indispensáveis:**
  - Armazenamento de credenciais e chaves de API secretas (arquivos `.env`) para evitar exposição pública de senhas.
  - Pastas de dependências gigantescas que podem ser reconstruídas localmente (como `node_modules/`).
  - Arquivos gerados automaticamente pelo sistema operacional ou pelo ambiente de desenvolvimento (como arquivos `.log` ou `.DS_Store`).
  - Pastas de recursos locais específicos de um integrante do grupo que não devem ser compartilhados (como a pasta `img/` exigida na nossa atividade).

---

### 8. Descreva o funcionamento dos comandos git pull e git push, explicando como ocorre a sincronização entre repositórios locais e remotos.

- **`git push`:** Pega os commits que você fez no seu repositório local e os envia para o repositório remoto (como o GitHub), atualizando a branch correspondente na nuvem para que seus colegas tenham acesso às suas alterações.
- **`git pull`:** Faz o oposto. Ele busca as alterações existentes no repositório remoto e, imediatamente, tenta mesclá-las (_merge_) na sua branch local atual. Na prática, o `git pull` é a combinação de dois comandos executados em sequência: `git fetch` (buscar) + `git merge` (unir).

---

### 9. Explique o que são conflitos de merge, como eles surgem e quais estratégias podem ser utilizadas para resolvê-los.

- **Como surgem:** Um conflito de merge acontece quando o Git tenta juntar duas branches, mas descobre que a mesma linha de um mesmo arquivo foi alterada de formas diferentes em ambas, ou que um arquivo foi deletado por uma pessoa e editado por outra. O Git não consegue decidir sozinho qual versão é a correta.
- **Estratégias de Resolução:**
  - O Git interrompe o processo e marca os arquivos em conflito.
  - O desenvolvedor deve abrir o arquivo afetado, analisar as marcações visuais geradas pelo Git (`<<<<<<< HEAD`, `=======`, `>>>>>>>`), decidir qual código manter (ou mesclar ambos manualmente) e apagar as marcações.
  - Após ajustar o arquivo no editor de código, roda-se `git add` e `git commit` para finalizar a integração de forma manual.

---

### 10. Discuta a importância do versionamento de código no desenvolvimento moderno de software, considerando manutenção, rastreabilidade e colaboração.

- **Manutenção:** Permite experimentar melhorias, refatorar códigos e testar novas tecnologias sem medo, sabendo que há uma rede de segurança estável para onde voltar se algo der errado.
- **Rastreabilidade:** Funciona como uma auditoria. É possível saber exatamente quem escreveu cada linha de código, quando mudou e o motivo daquela alteração.
- **Colaboração:** Transforma o desenvolvimento em um processo escalável, onde centenas de programadores espalhados pelo mundo podem construir e dar manutenção ao mesmo produto de forma organizada e simultânea.

---

### 11. Explique a finalidade de Pull Requests no GitHub e sua relevância para revisão de código e integração contínua.

- **Finalidade:** Um Pull Request (PR) é uma solicitação formal enviada na plataforma do GitHub para que as alterações feitas em uma branch isolada sejam integradas (mescladas) à branch principal do projeto (`main`).
- **Relevância:** É o espaço ideal onde ocorre a **Revisão de Código (Code Review)**, permitindo que outros membros do grupo comentem, sugiram melhorias e aprovem o código antes dele virar oficial. Também serve de gatilho para ferramentas de **Integração Contńua (CI)** rodarem testes automáticos de qualidade antes do merge final.

---

### 12. Descreva como o Git pode auxiliar na recuperação de versões anteriores de um projeto e na auditoria de alterações realizadas pela equipe.

- **Recuperação:** O Git disponibiliza comandos poderosos de viagem no tempo. Com o `git checkout` ou `git switch`, é possível navegar temporariamente para commits antigos. Com o `git revert`, cria-se um commit que desfaz exatamente o que um commit problemático passado causou. E com o `git reset`, pode-se limpar ou redefinir o histórico até um ponto específico.
- **Auditoria:** Com o comando `git log`, você visualiza a lista completa e cronológica de atualizações do software. Já o comando `git blame` permite inspecionar um arquivo linha por linha para ver o autor e o commit original de cada modificação.
