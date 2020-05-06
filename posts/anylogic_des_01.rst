.. title: Anylogic Simulação de Eventos Discretos - Parte 01
.. slug: anylogic_des_01
.. author: vstram
.. date: 2020/04/30
.. categories: pt-BR DES

Modelagem de um processo simplificado de manufatura, composto por uma única etapa, através do software Anylogic 8.5.2, utilizando a abordagem "Simulação de Eventos Discretos" (DES - Discrete Event Simulation). O processo consiste apenas uma máquina, processando um fluxo de matérias primas que podem ser acumuladas em uma fila de capacidade limitada.

.. TEASER_END

.. image:: /images/man-wearing-gray-shirt-and-welding-mask-covered-in-welding.jpg

.. sidebar:: Conteúdo

    .. contents::

========
Objetivo
========

Simular com o Anylogic 8.5.2 o processo de manufatura de um produto, composto de uma única etapa, utilizando a abordagem "Modelagem de Eventos Discretos"

=====================
Descrição do Processo
=====================

1. Processo inicia com a matéria prima sendo alimentada por fluxo constante de fornecimento;
2. A máquina processa esta matéria prima, transformando-a em produto final;
3. Esta matéria prima poderá se acumular em uma fila próxima à maquina;

=============
Considerações 
=============

1. Processo idealizado sem operadores. Uma vez que a matéria-prima se aproxima da máquina, esta é carregada instantaneamente para processamento. Da mesma forma, assim que a matéria-prima é transformada em produto acabado, este é transportado imediatamente para o estoque. Não há atrasos na carga/descarga de peças na máquina;
2. Não há variações de desempenho de produção da máquina (por desgaste das ferramentas ou peças). A máquina não necessita de reparos ou ajustes durante toda a produção. A energia fornecida pela rede elétrica se mantém estável e capaz de atender ao funcionamento da máquina;
3. A qualidade da materia-prima e do produto acabado após ser processado pela máquina são sempre considerados ideais. Não há refugos;
4. Não há variações na capacidade de fornecimento de matéria-prima.
5. Não há restrições de transporte, tanto da matéria prima para a máquina, como de produtos acabados depois da produção da máquina;
6. Dimensões e pesos, tanto da materia-prima como do produto acabado, não estão sendo considerados;

======================
Parâmetros do Processo 
======================

1. O taxa de fornecimento de materia prima é de um item por minuto;
2. A capacidade de acúmulo de peças de matéria prima próxima à máquina é de 50 itens;
3. A máquina é capaz de transformar a matéria-prima em produto acabado em um tempo constante de 60 segundos
4. A capacidade da máquina é de uma peça por vez.

============
Procedimento 
============

1. Crie um novo modelo no Anylogic. Atribua um nome, tal como: des01
2. Mude a unidade de tempo de segundos para minutos. Clique em 'Finish'
3. Usamos os blocos disponiveis na paleta 'Process Modeling Library' para modelar este processo. Inicie arrastando um bloco 'source' para a área de trabalho
4. Defina a propriedade 'Arrival Rate' do bloco source em 1 item por minuto;
5. Arraste um bloco 'queue' próximo ao bloco 'source'. Observe que automaticamente eles são conectados. Defina a propriedade 'Capacity' para 50;
6. Arraste um bloco 'delay' próximo ao bloco 'queue'. O bloco 'delay' vai modelar a máquina responsável pelo processamento da matéria prima em produto final. Defina a propriedade 'Delay Time' para 1 minuto
7. Arraste um bloco 'sink' próximo ao bloco 'delay'. O bloco 'sink' é usado para indicar o fim do processo;
8. A modelagem deste processo simplificado está feita. Inicie a simulação ao clicar no botão 'Run Simulation' na barra de ferramentas (ou tecle F5);
9. Aparece a tela de simulação. Nela, é possivel iniciar, pausar, interromper e ajustar a velocidade da simulação. Inicie a simulação ao clicar no botão 'Run'. Observe a variação dos números próximos a cada bloco. Eles indicam a movimentação dos itens na entrada, dentro do bloco e na saída do mesmo.

.. figure:: /images/des_01.png

    Imagem mostrando o Anylogic com o modelo processo e algumas telas de configuração

===================
Análise do Processo 
===================

Este processo foi modelado para representar um processo perfeitamente "equilibrado" (ou balanceado), o que seria o objetivo de todo gerente de produção. Embora excessivamente idealizado, permite estabelecer parâmetros de referência, quando comparamos com um processo real. Isto é, representa o limite máximo de performance ao qual o processo deve ser otimizado.

Tal raciocínio (comparação ideal x real) pode ser levado também a cada etapa do processo, de tal forma que seja possível pontuar a performance de cada etapa individualmente. Assim, uma vez que determinada etapa do processo apresenta uma performance muito abaixo da ideal, pode-se tomar medidas para verificar e corrigir o que for necessário. 

Observe que, durante a simulação, eventualmente ocorre a formação de uma pequena fila de peças. Isso ocorre porque, segundo a documentação, uma taxa de 'n' implica que:

    "os agentes são gerados na taxa de chegada especificada (que é equivalente ao tempo entre chegadas exponencialmente distribuído com média = 1 / n)"

Ou seja, não significa que uma peça é fornecida a cada 'n' minutos. Esta é a única concessão à intenção de modelar perfeitamente este processo. A intenção aqui era observar o comportamento da fila ao longo do tempo.

Nos próximos artigos, irei trazer este modelo à dura realidade enfrentada diariamente no chão de fábrica, adicionando gradativamente algumas das mais comuns dificuldades encontradas durante a manufatura de produtos. Irei adicionar também no modelo algumas formas de mensurar o desempenho do processo, pois não se pode controlar algo que não é medido. 

Até lá!

===============
Recursos usados 
===============

1. https://www.anylogic.com/ - Para modelar o processo de manufatura
2. https://www.gimp.org/ - Para editar as figuras



