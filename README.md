# Stryker Mutator

<br>

Documentação oficial: https://stryker-mutator.io/

<br>
<hr>
<br>

## Instalação global:

<br>

```
dotnet tool install -g dotnet-stryker
```

<br>

## Instalação no projeto:

<br>

Crie um arquivo chamado dotnet-tools.json na pasta do projeto se esta for sua primeira ferramenta local:

```
dotnet new tool-manifest
```

Em seguida, instale o stryker sem o sinalizador -g executando o seguinte comando na pasta do projeto:

```
dotnet tool install dotnet-stryker
```

Verifique o arquivo dotnet-tools.json no controle de origem.

Agora o resto de sua equipe pode instalar ou atualizar o stryker com o seguinte comando:

```
dotnet tool restore
```

<br>
<hr>
<br>

## Execução do Stryker

<br>

Vamos matar alguns mutantes.

Para a maioria dos projetos, nenhuma configuração é necessária. Basta executar o stryker e ele encontrará seu projeto de origem para sofrer mutação:

```
dotnet stryker

dotnet stryker -o
```

<br>

~/Source/Personal/netcore-todolist-api-template/Solution/Tests.Unit

```
dotnet stryker -p /Users/leandroandrade/Source/Personal/netcore-todolist-api-template/Solution/Core.Application/Core.Application.csproj

dotnet stryker -p /Users/leandroandrade/Source/Personal/netcore-todolist-api-template/Solution/Core.Application/Core.Application.csproj -o
```

<br>
<hr>
<br>

## Estados mutantes e métricas

<br>

Esta página deve esclarecer os diferentes resultados que um mutante pode ter e as diferentes métricas que você encontrará em qualquer relatório de teste de mutação.

Você é novo em testes de mutação, veja o que é teste de mutação?

<br>

### Estados mutantes:

Um mutante pode ter um dos seguintes estados:

<br>

<b>Morto:</b> 

Quando pelo menos um teste falhou enquanto este mutante estava ativo, o mutante é morto. É isso que você quer, bom trabalho!

<br>

<b>Sobreviveu:</b>

Quando todos os testes passaram enquanto este mutante estava ativo, o mutante sobreviveu. Está faltando um teste para isso.

<br>

<b>Sem cobertura:</b>

 O mutante não é coberto por um de seus testes e sobreviveu como resultado.

<br>

<b>Timeout:</b>

A execução de testes com este mutante ativo resultou em timeout. Por exemplo, o mutante resultou em um loop infinito em seu código. Não dê muita atenção a este mutante. É contado como "detectado". A lógica aqui é que, se esse mutante fosse injetado em seu código, sua compilação de CI o detectaria porque os testes nunca serão concluídos.

<br>

<b>Erro de tempo de execução:</b>

 A execução dos testes resultou em um erro (em vez de um teste com falha). Isso pode acontecer quando o executor de teste falha. Por exemplo, quando um executor de teste lança um OutOfMemoryErrorou para linguagens dinâmicas em que o mutante resultou em código não analisável. Não gaste muita atenção olhando para este mutante. Ele não é representado em sua pontuação de mutação.

 <br>

<b>Erro de compilação:</b>

 O mutante causou um erro de compilação. Isso pode acontecer em linguagens compiladas. Não gaste muita atenção olhando para este mutante. Ele não é representado em sua pontuação de mutação.

<br>

<b>Ignorado:</b>

O mutante não foi testado porque foi ignorado. Seja por ação do usuário ou por outro motivo. Isso não contará para sua pontuação de mutação, mas aparecerá nos relatórios.

<br>
<hr>
<br>

### Métricas:

Com base nesses estados, podemos calcular as seguintes métricas:

<br>

<b>Detectado killed + timeout</b>

O número de mutantes detectados por seus testes.

<br>

<b>Não detectado survived + no coverage</b>

O número de mutantes que não são detectados pelos seus testes.

<br>

<b>Coberto detected + survived</b>

O número de mutantes para os quais seus testes produzem cobertura de código.

<br>

<b>Válido detected + undetected</b>

O número de mutantes válidos. Eles não resultaram em um erro de compilação ou erro de tempo de execução.

<br>

<b>Inválido runtime errors + compile errors</b>

O número de mutantes inválidos. Eles não puderam ser testados porque produzem um erro de compilação ou um erro de tempo de execução.

<br>

<b>Total de mutantes valid + invalid + ignored</b>

Todos os mutantes.

<br>

<b>Pontuação de mutação detected / valid * 100</b>

A porcentagem total de mutantes que foram detectados. Quanto mais alto, melhor!

<br>

<b>Pontuação da mutação com base no código coberto detected / covered * 100</b>

A porcentagem total de mutantes que foram detectados com base nos resultados da cobertura do código.

<br>
<hr>
<br>

### Estados de teste e métricas:

Um teste também pode ter estado em relação ao teste de mutação.

<br>

<b>Matar</b>

O teste está matando pelo menos um mutante. Isso é o que você quer.

<br>

<b>Cobertura</b>

O teste cobre mutantes, mas não mata nenhum deles. As informações de cobertura devem estar disponíveis por teste para fornecer este estado de teste.

<br>

<b>Não cobrindo</b>

O teste não está cobrindo nenhum mutante (e, portanto, não está matando nenhum deles).

<br>

<b>Total</b>

Not covering + covering + killing Número total de testes.
