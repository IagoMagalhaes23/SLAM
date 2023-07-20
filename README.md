# SLAM


## Introdução ao SLAM
O SLAM é uma peça essencial da robótica que ajuda os robôs a estimar sua pose – posição e orientação – no mapa enquanto cria o mapa do ambiente para realizar atividades autônomas.

Imagine-se acordando em um lugar estranho. O que você faria? Você provavelmente começaria a olhar em volta para localizar onde está. Ao longo do caminho, você marcaria alguns objetos para ajudá-lo a lembrar para onde está indo. Você estaria fazendo um mapa mental, desenhando como o mundo se parece ao seu redor e onde você está nesse mundo. É isso que a Localização e Mapeamento Simultâneos (SLAM) faz.

**Localização** <br>
Quando um robô autônomo é ligado, a primeira coisa que ele faz é identificar onde está. Em um cenário típico de localização, um robô é equipado com sensores para escanear seus arredores e monitorar seus movimentos. Usando as entradas dos sensores, o robô é capaz de identificar onde está em um determinado mapa. Em alguns casos, um dispositivo de rastreamento como um GPS é usado para auxiliar no processo de localização (é assim que o Google pode fornecer o ponto azul no Google Maps, por exemplo).

**Mapeamento** <br>
Embora pareça simples, criar um mapa não é uma tarefa fácil, principalmente para um robô. Para começar, um tipo de detector visual, como uma câmera ou um sensor lidar, é usado para registrar os arredores. À medida que o robô se move, ele captura mais informações visuais e tenta fazer conexões e extrair recursos – como um canto – para marcar alguns pontos identificáveis. No entanto, alguns dos recursos podem parecer muito semelhantes e ser difícil para um robô distinguir qual é qual. É quando a localização se torna útil para criar mapas mais precisos via SLAM.

## Por que usar SLAM
O SLAM é útil para robôs autônomos, usando o exemplo do aspirador de pó. Imagine uma sala de estar típica onde há móveis grandes como um sofá que fica bem estacionário em seu local. itens menores, como uma mesa de centro que pode se mover pela sala com frequência e as paredes da sala que nunca se movem (a menos que você esteja no meio de uma grande reforma!). Para limpar a sala, o aspirador autônomo precisaria de um mapa para navegar pelo espaço. 

O mapa pode ser alimentado ao vácuo de diferentes maneiras. Uma maneira é criar e carregar manualmente o mapa na máquina, exigindo que você redesenhe o mapa sempre que uma peça de mobília for movida. Outro método é redesenhar o mapa novinho em folha toda vez que o aspirador é ligado, o que consumiria muitos recursos e seria ineficiente para um dispositivo doméstico remoto. É quando o SLAM brilha. 

Ao utilizar o SLAM, o aspirador é capaz de atualizar apenas os locais que foram alterados desde a varredura anterior. Como resultado, pode realizar o trabalho principal de varrer o chão com mais eficiência. Neste exemplo, o robô pode contar com as paredes para obter uma referência consistente, mas quando uma peça de mobília estiver em um local inesperado, o robô atualizará o mapa. Um benefício semelhante se aplica a outros robôs autônomos, como os robôs de entrega de última milha. O mapa geral da vizinhança pode ser fornecido aos robôs de entrega, mas os robôs podem responder a quaisquer novos objetos, como carros estacionados ou pedestres, que eles vejam com o SLAM. 

O SLAM também pode ser usado quando é impossível obter um mapa para começar - por exemplo, um poço de mina, túnel vulcânico ou Marte! Um robô autônomo é capaz de examinar essas condições desconhecidas, criar um mapa preciso e compartilhar os resultados com controladores para pesquisas ou explorações adicionais.

## SLAM baseado em câmera
Quando uma câmera é usada para capturar uma cena, ela é capaz de gravar imagens de alta resolução com detalhes ricos. Um algoritmo de visão computacional, como SIFT (transformada de recurso invariante em escala) ou ORB (RÁPIDO orientado e BRIEF rotacionado), pode ser usado para detectar recursos. Por exemplo, se um robô estiver usando uma câmera para mapear um armazém, as imagens gravadas podem ter paletes, prateleiras e portas. Ao examinar as diferenças de cor dos pixels vizinhos, o robô pode identificar que existem objetos diferentes na cena.

##  SLAM baseado em Lidar
Ao contrário do SLAM baseado em câmera, um sensor lidar coleta nativamente informações sobre a profundidade e a geometria dos objetos capturados na cena. Se o mesmo robô de armazém acima estivesse usando um sensor lidar em vez de uma câmera, ele usaria as distâncias e formas retornadas ao sensor para identificar objetos. Na verdade, um SLAM baseado em lidar usa arestas e planos gravados pelo dispositivo como recursos em vez de pixels vizinhos para conectar as informações visuais e criar um mapa. Ao contrário das câmeras, essa abordagem é muito melhor na criação de uma cópia digital gêmea do mapa em 3D, que é mais realista.

## Como escolher o SLAM certo
Existem vários métodos SLAM que funcionam de maneira bem diferente. Além disso, cada método tem vantagens e desvantagens dependendo dos casos de uso. Vejamos algumas distinções que ajudariam na decisão sobre um algoritmo SLAM. 

Uma categoria é a saída do algoritmo SLAM. Por exemplo, se você estiver em um parque, gostaria de saber a posição relativa de árvores e bancos (método topológico) ou as distâncias exatas entre eles (método métrico)? Além disso, você planeja recriar uma cópia digital do parque (método volumétrico) ou apenas informações suficientes para distinguir objetos (método baseado em recursos)? Como você pode imaginar, algumas saídas exigiriam recursos pesados ​​e até diferentes tipos de sensores para realizar o trabalho.

Outro fator é a natureza do ambiente. O local em que você está executando um algoritmo SLAM é um local estático que não mudará com o tempo ou um local dinâmico que exigiria atualizações? Imagine um robô andando por um corredor vazio em um armazém, mas encontrando pilhas de paletes no caminho de volta. Seria capaz de fechar o loop e fazer a conexão de que está no mesmo lugar, mas apenas com objetos diferentes adicionados?

Por último, mas não menos importante, está a instância de vários robôs. Quando há vários robôs navegando de forma autônoma dentro de um armazém, ele pode enfrentar diferentes desafios. Um desafio é a capacidade de criar um mapa limpo sem outros robôs. Como você garante que cada robô conheça as posições dos outros para poder excluí-los no mapeamento? Se os robôs podem se comunicar uns com os outros, cada robô pode criar mapas menores localmente e compartilhá-los com um sistema central para criar um mapa completo? 

Como você pode ver, não existe um único algoritmo SLAM que atenda a todos os casos de uso. No entanto, o SLAM ainda está evoluindo com os avanços da tecnologia. Para ter sucesso, é preciso entender verdadeiramente o caso de uso e ser flexível ao testar diferentes algoritmos para encontrar a melhor solução.

## O que vem depois do SLAM
No início, usamos o exemplo de acordar em um lugar estranho para explicar que SLAM é o ato de desenhar um mapa dos arredores e localizar onde você está no mapa. No entanto, isso exclui o “o quê” no mapa. Reconhecemos uma árvore quando a vemos, mas os robôs não. Precisamos que eles saibam que o objeto alto com pontos espalhados ao redor do centro na frente deles é na verdade uma árvore. Essa adição de semântica à saída SLAM pode aumentar o nível de autonomia que um robô pode alcançar. Por exemplo, um robô pode manobrar pelo armazém com mais segurança se puder identificar humanos e diminuir a velocidade perto deles para evitar acidentes por movimentos bruscos. 

Com os desenvolvimentos no aprendizado de máquina, a adição de semântica ao SLAM está se tornando mais acessível, expandindo ainda mais os casos de uso de AGVs e AMRs. Existem empilhadores autónomos que conseguem identificar uma palete e os seus orifícios para poder transportá-la, e escavadoras autónomas que se podem deslocar para locais específicos para escavar o solo.

## Projetos com SLAM

## SLAM com WebCam

## SLAM com Drone

## SLAM com robô

## Referência

- [Introduction to SLAM (Simultaneous Localization and Mapping)](https://ouster.com/blog/introduction-to-slam-simultaneous-localization-and-mapping/)
