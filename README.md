# Agile

Este é um repositório-guia para as práticas da metodologia ágil no versionamento de códigos. Siga o passo a passo abaixo quando for iniciar uma nova sprint ou task em seu projeto.

**1º passo:** Exclua localmente as branches das tasks da última sprint.

```
git branch --delete <nome da branch local 1> <nome da branch local 2> ... <nome da branch local n>
```

Se a(s) branch(es) não estiver(em) totalmente mergeada(s),

```
git branch -D <nome da branch local 1> <nome da branch local 2> ... <nome da branch local n>
```

**2º passo:** Atualize as branches remotas localmente.*

```
git remote update origin --prune
```

*Esse passo não é estritamente necessário. O que ele faz é atualizar, no prompt de comando, as branches existentes remotamente. Ao finalizarmos uma task, é normal que a branch da task em questão seja excluída após o merge. No entanto, isso não é refletido localmente quando utilizamos o comando `git branch -a` para visualizarmos as branches locais e remotas. Pode ser que a branch da task ainda apareça na lista como se existisse remotamente, o que já não seria o caso.

Para que o terminal faça essa atualização de forma automática,

```
git config remote.origin.prune true
```

**3º passo:** Cheque as atualizações nas branches locais e remotas.

```
git branch -a
```

**4º passo:** Crie localmente a branch da próxima sprint baseada na branch development.

```
git checkout -b <nome da branch local> <nome da branch remota>
```

Também é possível usar

```
git switch <nome da branch remota>
```

No primeiro caso, é possível atribuir um nome particular à branch local. Esse nome não precisa ser igual ao da branch remota. No último caso, o nome da branch local terá o mesmo da branch remota.

**5º passo:** Inicie uma task a partir da branch da nova sprint.

```
git checkout -b <nome da task>
```

As branches de tasks deverão sempre ser criadas a partir da branch da sprint. Esta nunca deverá guardar alterações, apenas após um code review ou ao final da sprint. A branch da sprint apenas servirá de base para a criação de branches de task e de referência para as alterações realizadas nas tasks em relação à última sprint.

**6º passo:** Na branch da task, ao finalizar a task, adicione os arquivos modificados (apenas aqueles que possuem relação com a task).

```
git add <nome do arquivo 1> <nome do arquivo 2> ... <nome do arquivo n>
```

Para adicionar todos os arquivos de uma vez, EXCETO os arquivos 1, 2, ..., n (referência genérica).

```
git add -- . :!<nome do arquivo 1> :!<nome do arquivo 2> ... :!<nome do arquivo n>
```

Para adicionar todos os arquivos, sem exceção,

```
git add .
```

**7º passo:** Commite suas alterações.

```
git commit -m "#<número da issue> <tipo de commit>: <mensagem do commit>
```

Por exemplo:

```
git commit -m "#1 feat: Adiciona menu lateral com opções de gerenciamento
```

No commit acima, #1 referencia a issue relativa à task, "feat" informa que o commit é de uma nova feature da aplicação e "Adiciona menu lateral com opções de gerenciamento" conceitua a feature.

**8º passo:** Suba a branch da task para o repositório remoto.

```
git push --set-upstream origin <nome da branch da task>
```

**9º passo:** Inicie uma nova task a partir da branch local da sprint.

```
git checkout <nome da sprint atual>
```

**10º passo:** Continue a partir do 4º passo.
