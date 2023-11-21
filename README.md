# LFA-TF2

Descrição do Trabalho:

A descrição deste Trabalho Final está relacionada com a linha de fabricação de automóveis.
Assim, uma linha de produção está associada a produção de um modelo específico de um carro. Ou seja, um modelo de um carro está associado a um formato específico, e características que o define. Normalmente, as montadoras associam siglas a um modelo, como XL, SL, etc.
O TF deste semestre envolve a modelagem de linhas de produção de 4 tipos específicos de carros, sendo que cada um deles deverá possuir entre 2 e 4 modelos distintos. Como exemplo, antigamente, carros (modelos) se diferenciavam por ter ou não direção hidráulica, ar-condicionado, etc.
Neste trabalho, você deverá modelar uma fábrica, através do uso de autômatos com pilha, associando-os (quando for necessário) com o conceito de autômatos com saída.
Outra característica que deverá estar presente, na sua modelagem, será a identificação de falhas na produção, com a emissão de relatórios diários, quanto a produção de veículos finalizados (quantitativamente, separando os tipos/modelos em seu relatório), bem como a situação dos veículos que não foram finalizados (seja por final de expediente, ou por falha na produção).
Os relatórios deverão ser emitidos com base no modelo utilizado para representar as etapas de fabricação, considerando aqueles veículos finalizados, bem como os demais, ainda em produção.
Como referência de modelagem, você deverá fazer uso de Autômatos com Pilha, podendo fazer uso do conceito de saída (aplicado a autômatos finitos, mas facilmente estendido para o modelo com pilha).
Lembre-se que você pode fazer uso de instâncias de um único modelo de AP, representando a situação da produção de uma unidade específica.
Assim, o seu código deverá apresentar a situação em cada "instante", bem como o relatório final de cada dia de produção.

Ideia do Trabalho:

Para começar a devemos definir os carros e seus modelos disponiveis seram eles os carros a, b, c e d.
Os modelos x, y e z ,além desses modelos ainda existe a chance de que ele apresente uma falha (representados pela letra f) ou esteja incompleta caso não haja tempo para terminar a produção (nesse caso esta representada pela letra i). 
Os carros seram associdos a uma sigla essa formada pelo nome do carro e seu modelo ex: ax, by, cf, di.
Outro valor importante é a capacidade de produção de carros que a fabrica pode realizar por dia (esse valor sera o valor da pilha, mas isso sera explicado posteriormente).
Para simular falhas de montagem utilizaremos um valor, que indica que a quantia de veiculos produzidos, que apresenta falha em sua montagem recebendo a letra "f" em sua sigla.
A primeira etapa é definir o número de carros que a empresa pode produzir por dia.
Ainda antes do inicio da produção é gerado um pedido (aleatorio ou não) dos veículos que devem ser produzidos no dia, para ao fim gerar um relatorio informando se o pedido foi atendido.
Caso este pedido seja escrito pelo usuario e não gerado de forma aleatoria, ele deve informar apenas o número e sigla do veiculo requisitado, por exemplo: 2ax 3by 1cy 2bz 1dy

Apertir disso o programa vai reescrever o pedido em um formato de fita que sera lido pelo automato que controla a linha de produção (logo sera explicada seu funcionamento).
a forma com que ele reescreve o pedido como fita é a sigla sucedida por "," ou "." em caso de virgula isso indica que exite outra sigla adiante e o ponto indica o fim da fita, fitas sem "." não seram aceitas. A escrita da fita divide o pedido pegando um elemento por vez e reagrupando para sua reescrita, pegando o exemplo de pedido acima iremos transforma-lo, tal qual o programa ira execulta-lo.

verifica se tem algum veiculo com valor diferente de 0
pedido: 2ax 3by 1cy 2bz 1dy fita:

primeiro ele separa um unidade da primeira sigla e diminui 1 de sua quantidade
pedido: 1ax 3by 1cy 2bz 1dy fita: ax

verifica se tem algum veiculo com valor diferente de 0
em seguida seleciona uma unidade da segunda sigla, acrescentando a "," para separa-la, visto que o teste acima foi verdadeiro
pedido: 1ax 2by 1cy 2bz 1dy fita: ax,by

refaz as verificações e seleções
pedido: 1ax 2by 0cy 2bz 1dy fita: ax,by,cy

refaz as verificações e seleções
pedido: 1ax 2by 0cy 1bz 1dy fita: ax,by,cy,bz

refaz as verificações e seleções
pedido: 1ax 2by 0cy 1bz 0dy fita: ax,by,cy,bz,dy

refaz as verificações 
após percorrer todo o pedido volta para o primeiro veículo do pedido
pedido: 0ax 2by 0cy 1bz 0dy fita: ax,by,cy,bz,dy,ax

refaz as verificações e seleções
pedido: 0ax 1by 0cy 1bz 0dy fita: ax,by,cy,bz,dy,ax,by

refaz as verificações
repare que em seguida o valor da proxima sigla é 0, nesse caso ele passa para a proxima sigla caso ela exista
pedido: 0ax 1by 0cy 0bz 0dy fita: ax,by,cy,bz,dy,ax,by,bz

refaz as verificações e seleções
pedido: 0ax 0by 0cy 0bz 0dy fita: ax,by,cy,bz,dy,ax,by,bz,by

verifica se tem algum veiculo com valor diferente de 0, o resultado é verdadeiro, deste modo acrescenta o "." a fita 
pedido: 0ax 0by 0cy 0bz 0dy fita: ax,by,cy,bz,dy,ax,by,bz,by.
terminando assim a reescrita para a fita

Apartir da fita o programa atraves do número de falhas ira atribuir as falhas a fita, para isso o programa escolhe aleatoriamente algumas da siglas para receber o "f" no lugar de seus modelos, como exemplo
fita: ax,by,cy,bz,dy,ax,by,bz,by. n de falha: 2
assim das 9 siglas 2 receberam o "f" se tornando falhas
fita: ax,by,cf,bz,dy,af,by,bz,by

Outro aspecto é sobre a quantia maxima de produção no dia, antes da produção o programa deve reler a fita e marcar todos os veiculos acima do limite de produção com um "i" em seu final
fita: ax,by,cf,bz,dy,af,by,bz,by n max de produção: 7
fita: ax,by,cf,bz,dy,af,by,bi,bi

Agora a fita esta pronta para ser lida pelo automato com pilha responsavél pela linha de produção
Antes de começar irei explicar qual a função da pilha desse automato ela pode empilhar apenas as letras "T" e "F" aonde "T" significa um veiculo montado com sucesso e "F" um veiculo que apresentou falha em sua montagem. A pilha tem um valor maximo sendo esse o número max de produção acrescido de um, ela so pode resultar pilhas com no maximo o valor maximo de produção, contudo ela contém um unidade a mais na pilha para não apresentar erros em decorrencia dos veiculos pedidos que não poderam ser montados no dia. 

