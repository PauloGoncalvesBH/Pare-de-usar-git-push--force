---
title: "Pare de usar git push --force"
published: true
description:
tags: ptbr, git
canonical_url:
cover_image:
series:
---

<!--- Acima está o cabeçalho, com as informações do seu post, edite-as de acordo com sua necessidade. Para saber mais: https://dev.to/p/editor_guide
Apague tudo que está abaixo dessa linha e escreva seu post --->

> **[Esse conteúdo é abordado no meu treinamento de conceitos de git](https://github.com/PauloGoncalvesBH/treinamento-git)**

## Reescrevendo a história da branch com segurança

Ao reescrever a história da nossa branch, com `git rebase`, por exemplo, costumamos utilizar o `git push --force`. Essa opção força o envio das alterações e substitui todas as alterações remotas pela versão local.

O grande perigo é que, se outra pessoa tiver enviado uma alteração no repositório remoto e que não estava na sua versão local, esse trabalho será totalmente perdido.

## `git push --force-with-lease`

Para evitar essa situação (e muita dor de cabeça), adote o uso de `git push --force-with-lease` em detrimento de `git push --force`.

Esta opção permite forçar o push sem o risco de sobrescrever acidentalmente o trabalho de outra pessoa.

Ele atualizará a branch remota APENAS se o histórico dela for igual ao histórico que você alterou localmente, caso contrário o `push` será rejeitado. Nesse caso, você terá que levar a alteração remota da outra pessoa para a sua branch local antes de tentar fazer o `git push --force-with-lease` novamente.

*Exemplo de `push` rejeitado com o alerta de `stale info` (informação velha):*

![O que acontece com push --force-with-lease](https://raw.githubusercontent.com/PauloGoncalvesBH/Pare-de-usar-git-push--force/trunk/images/mensagem-terminal.png)

Pronto 😃 agora você pode garantir que não irá apagar acidentalmente alteração que alguém possa ter dado `push` enquanto você reescreveu o histórico!

Para aprofundar no tema recomendo a própria [documentação do git sobre _git-push_](https://git-scm.com/docs/git-push).

> Don't rewrite public history unless you're really sure about what you're doing. And if you do, be safe and force-with-lease.

---

###### _Esse post está sendo versionado e hospedado no [Github](https://github.com/PauloGoncalvesBH/Pare-de-usar-git-push--force)_
