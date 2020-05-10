.. title: Anylogic Simulação de Eventos Discretos - Parte 02
.. slug: anylogic-simulacao-de-eventos-discretos-parte-02
.. author: vstram
.. date: 2020-05-06 17:16:47 UTC-03:00
.. categories: pt-BR DES
.. has_math: true

Eu havia comentado no artigo anterior - Anylogic Simulação de Eventos Discretos - Parte 01 - sobre uma forma de mensurar a performance do processo modelado no Anylogic 8.5.2. Neste artigo, irei mostrar como isso pode ser feito.

.. TEASER_END

.. image:: /images/burned-in-time-series.jpg

.. sidebar:: Conteúdo

    .. contents::

========
Objetivo
========

Mostrar como mensurar a performance de um processo modelado no Anylogic 8.5.2. Esta performance será avaliada através do tempo necessário para produzir uma peça, e também através da contagem de peças produzidas em um dia de trabalho. Usaremos gráficos para mostrar estes dados.

=====================
Descrição do Processo 
=====================

1. O processo é basicamente o mesmo do artigo anterior.

=============
Considerações 
=============

1. O início da medição deve ser antes das peças (matéria prima) entrarem na fila (antes do bloco ``queue``) e o final deve ser logo após a peças serem processadas pela máquina (após o bloco ``delay``);
2. A contagem das peças produzidas deve ser neste mesmo trecho do processo.
3. Visto que este processo é idealizado sem operadores, considerar uniformidade de performance de produção na máquina. O tempo para carregar a máquina com as peças, verificar, iniciar a operação, retirar e inspecionar a peça produzida é igual a zero (somente o tempo da maquina 'rodando' é considerado);

======================
Parâmetros do Processo 
======================

1. O tempo deverá ser medido em minutos.
2. O dia de trabalho deverá ser de ``8 horas`` trabalhadas = ``480 minutos``. A simulação deverá contemplar esse período.

============
Procedimento 
============

1. É mais fácil começar de um 'V0', isto é, de um ponto de partida conhecido e que sabemos que está funcionando. Este processo é idêntico ao processo descrito no artigo anterior. Assim, iremos usar o processo modelado anteriormente como ponto de partida. Abra o projeto ``des01`` no Anylogic. Crie um novo modelo no Anylogic. Atribua um nome, tal como: ``des02``
2. Em sua área de trabalho deverão aparecer duas abas ``Main``: uma em branco (referente ao ``des02``) e outra com o processo modelado anteriormante (referente ao ``des01``). Clique e arraste um retângulo de seleção, envolvendo todos os blocos e ligações de ``des01``. Copie (Crtl+c) e cole (Ctrl+v) no Main de ``des02``
3. Na paleta ``Process Modeling Library``, localize o bloco ``Time Measure Start``. Com o ``Main`` referente ao ``des02`` aberto, arraste este bloco para a interligação entre os blocos ``source`` e ``queue``. Garanta que as ligações seja refeitas (acontece automaticamente se voce posicionar novo bloco corretamente)
4. Faça o mesmo com o bloco ``Time Measure End``, mas desta vez o posicione entre os blocos ``delay`` e ``sink``.
5. Posicione os blocos na área de trabalho de tal forma que eles estejam um pouco mais distantes entre si, conforme figura abaixo.
6. Selecione o bloco ``timeMeasureEnd``. Na janela de propriedades, campo ``TimeMeasureStart blocks``, clique no botão ``+`` e selecione ``timeMeasureStart``. Isso irá definir corretamente o trecho do processo a ser considerado para a contagem do tempo.

.. figure:: /images/des_02-a.png

    Observe o posicionamento dos blocos de tempo e também a configuração correta do bloco ``timeMeasureEnd``

7. Clique com o botão direito no bloco ``timeMeasureEnd`` e escolha ``Create Chart -> distribution``. Dimensione e posicione o gráfico gerado como achar melhor. Este gráfico irá mostrar um histograma com a distribuição dos tempos de produção no trecho do processo considerado.
8. Agora vamos avaliar o número de peças produzidas. Localize na paleta ``Analysis`` o bloco ``Dataset`` e o arraste para a área de trabalho.
9. Com o novo bloco ``dataset`` selecionado, localize na janela de propriedades o campo ``Vertical axis value`` e o defina como:

.. code-block:: java
    
    sink.count()

10. Esta instrução irá contar o número de peças que chegam ao bloco ``sink``. Repita o procedimento, criando um novo bloco ``Dataset``, mas desta vez defina o campo ``Vertical axis value`` como:

.. code-block:: java

    source.count()

11. Analogamente, esta instrução serve para contar as peças que são geradas pelo bloco ``source`` (nossa fonte de matéria prima). Para visualizar as informações geradas pelos datasets que criamos, arraste um gráfico ``Time Plot`` da paleta ``Analysis`` para a área de trabalho;
12. Observe que o gráfico vem preenchido com dois conjuntos de dados de exemplo. Usaremos os dois. No primeiro conjunto de dados, marque a opção ``Data set`` e defina o campo ``Data set:`` como ``dataset`` (que é o nome default do bloco que criamos no passo 8)
13. Repita o procedimento para o segundo conjunto de dados, mas defina o campo ``Data set:`` como ``dataset1`` (que é o nome default do bloco que criamos no passo 10) 
14. Ao mostrar resultados, é importante ser absolutamente claro nas informações presentes nos gráficos. Para melhorar o entendimento, defina o campo ``Title`` em no primeiro conjunto de dados como ``Machine Production``, e o segundo conjunto de dados como ``Delivery of Raw Material``

.. figure:: /images/des_02-b.png

    Configuração do gráfico

15. Finalmente, vamos definir o tempo máximo de simulação para nosso processo. Em ``Projects``, selecione o item ``Simulation:Main``. No grupo ``Model Time``, defina ``Stop at specified time`` no campo ``Stop:``. Em ``Stop Time:``, defina o valor 480.  
16. Pronto. O modelo está pronto para ser simulado. Tecle ``F5`` e depois clique em ``Run``.
17. [Opcional] Pode ser interessante ver graficamente a utilização da fila (número visível no bloco queue). Crie um novo bloco ``Dataset`` e defina o campo ``Vertical axis value`` como:

.. code-block:: java

    queue.size()

18. [Opcional] Arraste um gráfico ``Time Plot`` da paleta ``Analysis`` para a área de trabalho. Defina o campo ``Dataset`` como ``dataset2`` (que é o nome default do bloco que criamos no passo 17). Nomeie o gráfico como ``Queue Size``. Remova o conjunto de dados extra criado: selecione o ``Dataset`` inferior e clique no botão 'Remove'

===================
Análise do Processo 
===================

O video abaixo mostra a gravação da simulação do processo modelado no Anylogic:

.. raw:: html

    <video src="/videos/des02.mp4" width="1094" height="738" controls preload></video>

Apesar de simples, o processo modelado nesta simulação nos permite observar fenômenos muito interessantes. Note o comportamento das curvas ``Delivery of Raw Material`` e ``Machine Production``. Esta última foi modelada como uma produção constante de 1 peça por minuto, enquanto que a disponibilidade de materia prima foi modelada aleatoriamente através de um rate (taxa) de 1 peça por minuto em média. De acordo como o livro "Anylogic in Three Days":

    Rate (taxa): Usado para programar mudanças de estado esporádicas com um tempo médio conhecido. (...) o intervalo de tempo é determinado por uma distribuição exponencial parametrizada com a taxa dada. Por exemplo, se a taxa é de 0.2, os intervalos terão valores médios de 1/0.2 = 5 unidades de tempo

.. figure:: /images/exp-1.png

No caso modelado neste processo, foi atribuída a distribuição de probabilidade exponencial mostrada acima para a disponibilização de matéria prima, com intervalos de tempo variando aleatoriamente em torno de um minuto (``lambda = 1``). Esta distribuição é definida como:

.. math::

    f(x,\lambda)=\begin{cases}
    \lambda e^{-\lambda x} & \text{ if } x \geq  0 \\ 
    0 & \text{ if } x < 0 
    \end{cases}

Observa-se no vídeo que na maior parte do tempo há a formação de uma fila de peças (a curva cinza esta sempre um pouco acima da curva verde), devido à disponibilidade de peças a um ritmo maior que ``1`` peça por minuto.

Eventualmente (próximo ao minuto ``150``), o fornecimento de materia prima não consegue suprir a capacidade de produção (``queue = 0``) e a curva verde muda sutilmente sua inclinação para em seguida, rapidamente, obter novamente certa folga no envio de matéria prima. No pior momento, a fila fica em torno de ``24`` peças, atrasando bastante o tempo medido das peças seguintes que entram no processo. Como resultado, obtemos um tempo médio final de ``7.71`` minutos. 

A máquina não consegue compensar eventuais matérias primas disponíveis antes do tempo de ``1`` minuto, o que acaba por acumular para as peças seguintes. O atraso no tempo total se refere, portanto, aos pequenos atrasos que vão se acumulando ao longo do tempo.

A lição que fica é que se deve conhecer o comportamento (digo, distribuição de probabilidade) de cada etapa do processo e, caso tenha processos de "cauda longa" (isto é, que consomem muito tempo, mas em poucas ocorrências), ser capaz de ter na sequência do processo etapas que consigam compensar atrasos sem prejudicar muito o tempo total de produção. Há um elevado risco de acúmulo de peças em processamento na linha caso não seja possível compensar eventuais atrasos de etapas anteriores.

Se o fornecimento de matéria prima fosse perfeito, isto é, no mesmo ritmo da produção da máquina ``constante = 1 peça por minuto`` teria-se uma produção de 480 peças. No vídeo constatamos que foram produzidas 462 pelas. Há um indicador de eficiência denominado OEE (Eficiência Global dos Equipamentos), utilizado para "qualificar e indicar a maneira como a operação de fabricação é realizada e auxilia na melhoria dos processos de manutenção e produção da empresa". É definido como:

.. math::

    OEE=availability \times productivity \times quality

Onde:

.. math::

    availability=\frac{production\, time}{available\, time} \times 100
    
.. math::

    productivity=\frac{real\, production}{theoretical\, production} \times 100
    
.. math::

    quality=\frac{quality\, production}{total\, production} \times 100


Pelas simplificações descritas na Seção Considerações, tem-se que ``availability = 100%`` e ``quality = 100%`` 

.. math::

    OEE = \left ( 1.0 \times \frac{462}{480} \times 1.0 \right ) \times 100 = 96.25%

Uma OEE de ``96.25%`` é um valor excelente. Entretanto, considerando que este processo consiste de somente de uma etapa e que apenas o fornecimento de matéria prima tem um comportamento aleatório, imagine o quão desafiador poderá ser manter este OEE em um processo composto de múltiplas etapas.

E é isso! Nos próximos artigos continuaremos a trazer algumas complexidades para o processo modelado. Até lá!

========
Recursos
========
1. Para modelar o processo de manufatura - https://www.anylogic.com/
2. Para editar as figuras - https://www.gimp.org/
3. Royality free images - https://pt.freeimages.com
4. Para capturar o video da simulação do processo - https://screencast-o-matic.com/
5. AnyLogic in Three Days: Modeling and Simulation Textbook - Ilya Grigoryev - https://www.anylogic.com/resources/books/free-simulation-book-and-modeling-tutorials/
6. Para editar equações LaTex online - https://www.codecogs.com/latex/eqneditor.php
7. Para fazer o download do arquivo deste processo modelado no Anylogic - `Clique Aqui </anylogic/DES02/DES02.alp>`_
