**Instituto Federal de Santa Catarina - IFSC/Florianópolis**

**Alunos:** Greicili dos Santos Ferreira e Matheus Locatelli

**Unidade Curricular:** Projeto Integrador II

## **CONCEPÇÃO**
A situação de se ter um vazamento de água é algo comum e, em alguns casos, de difícil
detecção. Um exemplo típico que pode ser citado é a válvula de descarga do banheiro que
ficou acionada após o uso. Na maioria das vezes esse problema é descoberto tarde demais,
quando chega a fatura de água.

Com o objetivo de atender a essa necessidade, pensou-se em um sistema de monitoramento
de vazão da água que identifique os vazamentos e gere avisos ao usuário. Deste modo, é
possível realizar uma intervenção em um tempo menor, prevenindo maiores danos tanto
financeiro quanto para a sociedade, pois evita-se o desperdício de água potável.

O diferencial deste projeto é ser um sistema de monitoramento constante e que ajude o
usuário a detectar a presença de um vazamento, sem a necessidade de que o mesmo precise
ficar conferindo o medidor do distribuidor de água.

A ideia é observar a presença de uma vazão constante no ramal de entrada da residência
durante um tempo determinado pelo usuário. Há a possibilidade de colocar o sensor em mais
pontos, realizando o monitoramento de forma individualizada para cada setor da casa, de
acordo com o desejo do cliente. A detecção de vazamento será informada através de um sinal
sonoro e de uma interface, que exibirá uma mensagem de alerta para o usuário no seu celular ou no site.


**FIGURA 1 - CONCEPÇÃO DO PROJETO**
![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/b624517c-89d1-40b9-bcfe-cd24b6570c51)


## **DESIGN**
O funcionamento do projeto consiste em realizar o monitoramento da vazão de água na
entrada da residência por meio de um sensor de fluxo em conjunto com um dispositivo de
controle. Esse dispositivo será responsável por fazer o processamento dos dados e
encaminhar o resultado ao usuário, mantendo-o atualizado da condição do sistema. Na Figura
2, é apresentado um fluxograma que mostra as etapas para o funcionamento do sistema.

**FIGURA 2 - FLUXOGRAMA DO PRINCÍPIO DE FUNCIONAMENTO DO SISTEMA DO PROJETO**
![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/3335e96e-5513-4ed9-986f-73d3f027b40e)

Para o desenvolvimento do projeto será utilizado os seguintes materiais:
* Módulo Wifi ESP 8266;
* Sensor de Fluxo de Água 1/2" YF-S201b:
 ** Tipo de sensor: Efeito Hall
 ** Tensão de operação: 5-24V
 ** Corrente máxima: 15mA (5V)
 ** Faixa de fluxo: 1-30L/min
 ** Pressão máxima: 2,0 MPa
 ** Pulsos por litro: 450
 ** Frequência (Hz) = 7,5*Fluxo(L/min)
 ** Exatidão: 10%
 ** Dimensão conexão: 1/2ʺ
 ** Dimensão diâmetro interno: 0,78ʺ
 ** Dimensão externa: 2,5ʺ x 1,4ʺ x 1,4ʺ
* Display OLED I2C;
* Módulo Relé;
* Buzzer.

 
**FIGURA 3 - COMPONENTES NECESSÁRIOS**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/d0d556ce-439e-4c2e-9e86-01b5f263512e)

O sensor de fluxo YF-S201b fornece um sinal PWM com o número de pulsos de acordo com a
quantidade de água que passa em seu interior. Segundo a especificação do componente, um
litro equivale a 450 pulsos. A contagem dos pulsos será feita a cada segundo e o fluxo
calculado será apresentado ao usuário através do display OLED I2C .

O sensor de fluxo estará conectado a um microcontrolador ESP-8266, que será responsável
por realizar os cálculos que permitam saber a vazão de água na entrada da residência e por
interromper o fluxo, caso o usuário escolha esta opção. Outro ESP-8266 será utilizado para
atuar como a central do sistema, recebendo informações do ESP conectado ao sensor de fluxo
e encaminhando esses resultados para as interfaces com o usuário. A troca de dados entre os
dois ESPs será realizada através do protocolo de comunicação ESP-NOW, no qual ocorre a
comunicação direta entre as duas placas, sem a necessidade de utilizar um roteador. 
Quando um vazamento for detectado pelo sistema, o usuário receberá o aviso por meio de um
sinal sonoro, com a utilização do buzzer, e através de uma mensagem apresentada nas
interfaces com o usuário.

**FIGURA 4 - MAQUETE ELETRÔNICA**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/62f21d8c-9526-4456-84ae-2e5e1fdd573d)


### **INTERFACES COM O USUÁRIO UTILIZANDO O BLYNK**
O usuário poderá monitorar o sistema de forma remota utilizando os recursos oferecidos pelo
Blynk, que é uma plataforma que fornece opções para a visualização de dados e acionamento
de dispositivos com a criação de dashboards personalizáveis, como mostrado na Figura 5. O
acesso pode ser feito através do celular, com o aplicativo disponível na AppStore e na PlayStore,
e também pelo computador, através do site do Blynk.

**FIGURA 5 - APLICATIVO PARA VISUALIZAR OS DADOS PELO CELULAR E NAVEGADOR**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/4b0fcc6f-e0c1-449b-94f2-09c1b4ac5ccf)

Na Figura 6, é apresentada uma configuração inicial das possíveis informações que podem
estar disponíveis para o usuário que utilizará o sistema.

**FIGURA 6 - PROTÓTIPO NO BLYNK WEB**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/63a77dfe-dd00-4186-a4d4-b1c456d9df18)


## **IMPLEMENTAÇÃO**
A ideia do projeto é desenvolver um sistema que consiga detectar uma vazão constante, o que
indicaria a presença de um possível vazamento de água. A interação do usuário com o sistema
será estabelecida através de um equipamento instalado no interior da residência e da
utilização de um aplicativo de monitoramento, o Blynk, que oferece uma interface web e
mobile.

A implementação será realizada com a utilização de dois ESP 8266, sendo que um deles
atuará como uma central, conectado ao Blynk, enquanto o outro realizará o controle do fluxo,
informando à central quando um vazamento for detectado. A comunicação entre os EPSs será
estabelecida através do protocolo ESP-NOW, desenvolvido pela Espressif, e não necessita da
utilização de um roteador.

**Figura 7 - Comunicação entre os ESPs utilizando ESP-NOW**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/7fc59aa0-b9fb-498f-a95f-3c0007b9a11c)

Na Figura 8 é apresentado um esquema das atribuições de cada ESP-8266 no
funcionamento do sistema.

**Figura 8 - Atruibuição de cada ESP-8266**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/1c007764-f877-49b2-881f-17bbec6d1fe2)


### **ESP-SENSOR**
Na Figura 9, é apresentado o esquema de ligação dos componentes ao ESP-8266, que está
atuando como ESP-SENSOR.

**Figura 9- Maquete eletrônica para o ESP-SENSOR no Fritzing**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/6dd95f9f-1756-4782-848d-df7ee7915e2d)

O script desenvolvido para implementar as funções do ESP-SENSOR pode ser encontrado
[aqui](https://github.com/Greicili/PI2-Deteccao_vazamento/blob/main/ESP-SENSOR). Esse script contém o algoritmo para o cálculo da vazão, detecção de vazamento,
acionamento do rele e comunicação entre os ESPs.

### **ESP-CENTRAL**
Na Figura 10, mostra-se a montagem do esquema desenvolvido para o funcionamento do ESP-CENTRAL.

**Figura 10- Maquete eletrônica para o ESP-CENTRAL no Fritzing**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/ad308250-5c05-4244-acea-ad1cce406983)

O script desenvolvido para implementar as funções do ESP-CENTRAL pode ser encontrado
[aqui](https://github.com/Greicili/PI2-Deteccao_vazamento/blob/main/ESP-Central). Esse script é responsável por enviar os dados para o Blynk, realizar a comunicação entre
os ESPs e controlar o acionamento do buzzer.


### **BLYNK**
Os dashboards desenvolvidos no Blynk, para a versão web e mobile, é mostrado na Figura 11.

**Figura 11- Dashboards no Blynk**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/f0c30ddc-ec04-4ab8-9ac9-9ed52db3a5b4)

### **PROJETO FINAL**
A seguir é apresentado o resultado final da implementação do projeto. Na Figura 12,
encontra-se a estrutura criada para testar o funcionamento do sistema. A caixa preta serve
para armazenar a água que será utilizada para criar o fluxo que passará pelo sensor.

**Figura 12 - Projeto Final**

![image](https://github.com/Greicili/PI2-Deteccao_vazamento/assets/81031562/0dbf6f8f-31ca-4bee-8fbc-d5ef948176ca)

### **Vídeo - Projeto Final em funcionamento**
No [vídeo](https://github.com/Greicili/PI2-Deteccao_vazamento/blob/main/Video_Projeto_final_PI2.mp4) é mostrado a detecção do vazamento após ter sido identificado a presença de um
fluxo constante por um intervalo de 30 segundos. Lembrando que esse tempo para a detecção é definido pelo usuário.





## **REFERÊNCIAS**
SERRANO, Tiago Medicci. **Introdução ao Blynk App**. EMBARCADOS. Disponível em:
https://www.embarcados.com.br/introducao-ao-blynk-app/. Acesso em: 10 maio 2022

ESP-NOW Two-Way Communication Between ESP8266 NodeMCU Boards. Elaborado por
Random Nerd Tutorials. Disponível em: https://randomnerdtutorials.com/esp-now-two-way-communication-esp8266-nodemcu/. Acesso em: 19 jun. 2022.

LOUSADA, Ricardo. **Guia Prático do Sensor de Fluxo de Água**. 2021. Disponível em:
https://blog.eletrogate.com/sensor-de-fluxo-de-agua/. Acesso em: 13 jun. 2022.

Robocore. **Automação residencial utilizando o NOVO Blynk**. YouTube, 10 fev. 2022.
Disponível em: https://www.youtube.com/watch?v=Hez20pleimI. Acesso em: 02 jun. 2022.
