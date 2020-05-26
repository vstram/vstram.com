.. title: Anylogic: Simulação de Eventos Discretos - Parâmetros - Parte 03
.. slug: anylogic-simulacao-de-eventos-discretos-parte-03
.. author: vstram
.. date: 2020-05-11 17:14:30 UTC-03:00
.. tags: pt-BR, Simulação de Eventos Discretos

Nos artigos anteriores foi apresentada a modelagem no Anylogic de um sistema simplificado de manufatura, composto de uma única etapa. Além disso, introduzimos uma forma de mensurar a performance deste sistema, ao registrar o tempo de produção e a contagem de peças manufaturadas. No presente artigo mostraremos como parametrizar este sistema para que seja possível alterar algumas variáveis e analisar o impacto destas alterações no processo durante a simulação do modelo.

.. TEASER_END

.. sidebar:: Conteúdo

    .. contents::

========
Objetivo
========

Parametrizar o processo modelado no Anylogic 8.5.2 de modo que seja possível alterar variáveis do processo durante a simulação do modelo, permitindo assim analisar o comportamento do sistema em condições diferentes daquelas escolhidas inicialmente.

=====================
Descrição do Processo 
=====================

1. O processo é basicamente o mesmo do artigo anterior.

=============
Considerações 
=============

1. Deve-se permitir alterar a taxa de disponibilização de matéria prima e o tempo de produção na máquina;
2. Tal variação deve respeitar limites pré-estabelecidos.

======================
Parâmetros do Processo 
======================

1. Taxa de disponibilização de matéria prima: ``exponencial, valor inicial = 1 peça/min``, permitir uma variação de ``+/- 15%``;
2. Capacidade de produção da máquina: ``constante, valor inicial = 1 peça/min``, permitir variação de ``+/- 50%``.

============
Procedimento 
============

1. Abra o projeto do Anylogic ``des02``. Salve-o com outro nome: ``des03``. Assim, conseguiremos continuar da onde paramos;
2. A partir da paleta ``Agents``, arraste um bloco ``Parameter`` na area de trabalho. Atribua o nome: ``sourceRawMaterial``;
3. No campo ``Type``, escolha ``Double``;
4. No campo ``Default value``, defina ``1``
5. Arraste um novo bloco ``Parameter`` próximo ao anterior, mas desta vez atribua o nome: ``machineProduction``. Repita os passos ``3`` e ``4`` anteriores para este parâmetro criado. 
6. Agora iremos vincular estes parâmetros os blocos ``source`` e ``machine`` criados nos artigos anteriores. Selecione o bloco ``source`` e defina ``sourceRawMaterial`` em ``Arrival rate``;
7. Selecione o bloco ``delay`` e defina ``machineProduction`` em ``Delay time``;
8. Finalmente, iremos criar os controles de interface gráfica que permitirão modificar os valores dos parâmetros durante a simulação. Para isso, usaremos a paleta ``Controls``. Arraste o controle ``Slider`` próximo ao parâmetro ``sourceRawMaterial``.
9. Atribua o nome: ``slider_sourceRawMaterial``. Marque a caixa de seleção ``Link to:``, e escolha ``sourceRawMaterial`` na lista.
10. No campo ``Minimum value`` defina ``0.85``. E em ``Maximum value``, defina ``1.15``. Este é o intervalo que o controle slider irá permitir que o parâmetro ``sourceRawMaterial`` varie.
11. Arraste outro controle ``Slider``, desta vez próximo ao parâmetro ``machineProduction``, e atribua o nome: ``slider_machineProduction``. Marque a caixa de seleção ``Link to:``, e escolha ``machineProduction`` na lista.
12. No campo ``Minimum value`` defina ``0.5``. E em ``Maximum value``, defina ``1.5``. Este é o intervalo que o controle slider irá permitir que o parâmetro ``machineProduction`` varie.

.. image:: /images/des_03.png

13. Pronto! Inicie a simulação com ``F5`` e depois clique em ``Play``.
14. Durante a simulação é possível ajustar os valores dos parâmetros dentro dos limites pré-estabelecidos. Modifique e observe os resultados através dos gráficos. 

===================
Análise do Processo 
===================

O video abaixo mostra a gravação da simulação do processo modelado no Anylogic:

.. raw:: html

    <video src="/videos/des03.mp4" width="1094" height="738" controls preload></video>

Através dos controles ``slider``, é possível modificar os parâmetros previamente definidos para este processo, dentro dos limites permitidos. Após o inicio da simulação, observe o impacto da variação dos parâmetros no gráfico de distribuição dos tempos de produção e no gráfico que acompanha a quantidade de peças que passam pelos blocos ``source`` e ``delay``. O tamanho da fila de peças é o resultado mais visível da alteração dos parâmetros. Eventualmente, a fila chega perto do limite de ``50`` peças, quando rapidamente é feita uma modificação no parâmetro ``machineProduction``, reduzindo o tempo de produção para consumir o excesso de peças na fila.

Pode-se criar parâmetros não somente relacionados ao processo em si (capacidade de fornecimento/transporte de matéria prima, capacidade de produção de uma máquina), mas também parâmetros relacionados a custos, por exemplo.

Se para este processo simplificado já é possível fazer várias análises interessantes, imagine para um modelo de uma complexa linha de produção, em que o gestor necessita avaliar o impacto de uma modificação e apresentar os resultados desta modificação em uma reunião com diretores. Certamente uma simulação bem feita pode auxiliar no convencimento de uma alteração na linha de produção.

E é isso! Nos próximos artigos continuaremos a trazer algumas complexidades para o processo modelado. Até lá!

========
Recursos
========
1. Para modelar o processo de manufatura - https://www.anylogic.com/
2. Para editar as figuras - https://www.gimp.org/
3. Para capturar o video da simulação do processo - https://screencast-o-matic.com/
4. Para fazer o download do arquivo deste processo modelado no Anylogic - `Clique Aqui </anylogic/DES03/DES03.alp>`_


