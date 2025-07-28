# Entendendo Wireshark
O Wireshark é uma ferramenta de análise de pacotes de rede multiplataforma e de código aberto, capaz de detectar e investigar tráfego em tempo real e inspecionar capturas de pacotes (PCAP). É comumente usada como uma das melhores ferramentas de análise de pacotes. Nesta sala, veremos os fundamentos do Wireshark e o utilizaremos para realizar análises fundamentais de pacotes.

* Detectar e solucionar problemas de rede, como pontos de falha de carga da rede e congestionamento.
* Detectar anomalias de segurança, como hosts invasores, uso anormal de portas e tráfego suspeito.
* Investigar e aprender detalhes do protocolo, como códigos de resposta e dados de carga útil.

<img width="1463" height="633" alt="image" src="https://github.com/user-attachments/assets/60aebbe1-12cb-469f-859b-61421f3144ff" />

Além das informações rápidas sobre pacotes, o Wireshark também colore os pacotes em ordem de diferentes condições e o protocolo para detectar anomalias e protocolos em capturas rapidamente (isso explica por que quase tudo está verde nas capturas de tela fornecidas). Essa rápida olhada nas informações dos pacotes pode ajudar a rastrear exatamente o que você está procurando durante a análise. Você pode criar regras de cores personalizadas para identificar eventos de interesse usando filtros de exibição, e abordaremos esses detalhes na próxima sala. Agora, vamos nos concentrar nos padrões e entender como visualizar e usar os detalhes dos dados representados.

O Wireshark possui dois tipos de métodos de coloração de pacotes: regras temporárias, disponíveis apenas durante uma sessão do programa, e regras permanentes, salvas no arquivo de preferências (perfil) e disponíveis para a próxima sessão do programa. Você pode usar o "menu do botão direito" ou o menu "Exibir --> Regras de Coloração" para criar regras de coloração permanentes. O menu "Colorir Lista de Pacotes" ativa/desativa as regras de coloração. A coloração temporária de pacotes é feita com o "menu do botão direito" ou com o menu "Exibir --> Filtro de Conversa".

<img width="1463" height="657" alt="image" src="https://github.com/user-attachments/assets/da512377-e5b8-4889-aa65-f11b266ea589" />

O Wireshark pode combinar dois arquivos pcap em um único arquivo. Você pode usar o menu "Arquivo --> Mesclar" para mesclar um pcap com o arquivo processado. Ao escolher o segundo arquivo, o Wireshark mostrará o número total de pacotes no arquivo selecionado. Ao clicar em "Abrir", ele mesclará o arquivo pcap existente com o escolhido, criando um novo arquivo pcap. Observe que você precisa salvar o arquivo pcap "mesclado" antes de trabalhar nele.

Conhecer os detalhes do arquivo é útil. Especialmente ao trabalhar com vários arquivos pcap, às vezes você precisará saber e lembrar os detalhes do arquivo (hash do arquivo, hora da captura, comentários do arquivo de captura, interface e estatísticas) para identificá-lo, classificá-lo e priorizá-lo. Você pode visualizar os detalhes acessando "Estatísticas --> Propriedades do Arquivo de Captura" ou clicando no ícone pcap localizado no canto inferior esquerdo da janela.

## "Dissecação" de pacotes
A dissecação de pacotes também é conhecida como dissecação de protocolos, que investiga detalhes dos pacotes decodificando os protocolos e campos disponíveis. O Wireshark suporta uma longa lista de protocolos para dissecação, e você também pode escrever seus próprios scripts de dissecação.

## Detalhes de pacotes
Você pode clicar em um pacote no painel de lista de pacotes para abrir seus detalhes (um clique duplo abrirá os detalhes em uma nova janela). Os pacotes consistem em 5 a 7 camadas, com base no modelo OSI.
A imagem abaixo mostra a visualização do pacote número 27.

<img width="960" height="560" alt="image" src="https://github.com/user-attachments/assets/4dd05f72-1ee4-43d8-9f8e-eacb374d55d7" />

### Camadas OSI utilizadas pelo Wireshark

* **Frame (Camada 1): Isso mostrará qual frame/pacote você está vendo e detalhes específicos da camada Física do modelo OSI.**

<img width="687" height="358" alt="image" src="https://github.com/user-attachments/assets/4a6d5356-ab55-4d61-88b4-420f1e372ed4" />

* **Origem [MAC] (Camada 2): Isso mostrará os endereços MAC de origem e destino da camada de enlace de dados do modelo OSI.**

<img width="809" height="82" alt="image" src="https://github.com/user-attachments/assets/ff1d31df-e87a-4c94-bd71-f62e4f963881" />

* **Origem [IP] (Camada 3): Isso mostrará os endereços IPv4 de origem e destino da camada de rede do modelo OSI.**

<img width="643" height="304" alt="image" src="https://github.com/user-attachments/assets/d41e3e4a-ec8d-4752-9fd0-10ae414a1a7a" />

* **Protocolo (Camada 4): Isso mostrará detalhes do protocolo usado (UDP/TCP) e portas de origem e destino; da camada de Transporte do modelo OSI.**

<img width="779" height="365" alt="image" src="https://github.com/user-attachments/assets/84ead517-8e22-4c9a-bead-a9010d458ad9" />

* _Erros de protocolo: esta continuação da 4ª camada mostra segmentos específicos do TCP que precisaram ser remontados._

<img width="650" height="120" alt="image" src="https://github.com/user-attachments/assets/98386f17-1650-4573-9302-13a65c71c17b" />

* **Protocolo de Aplicação (Camada 5): Mostrará detalhes específicos do protocolo utilizado, como HTTP, FTP e SMB. Da camada de Aplicação do modelo OSI.**

<img width="847" height="267" alt="image" src="https://github.com/user-attachments/assets/59ecd13a-2bff-4404-81b1-41115988fcd7" />

# Navegação nos pacotes
## Números de Pacotes

O Wireshark calcula o número de pacotes investigados e atribui um número exclusivo para cada pacote. Isso auxilia no processo de análise de capturas grandes e facilita o retorno a um ponto específico de um evento.

## Ir para Pacote
Os números de pacotes não apenas ajudam a contar o número total de pacotes ou facilitam a localização/investigação de pacotes específicos. Este recurso não apenas navega entre os pacotes para cima e para baixo, como também fornece rastreamento de pacotes dentro do quadro e encontra o próximo pacote na parte específica da conversa. Você pode usar o menu "Ir" e a barra de ferramentas para visualizar pacotes específicos.

<img width="965" height="568" alt="image" src="https://github.com/user-attachments/assets/e7760722-fb67-46f4-9aae-4666d7037a1a" />

## Encontrar Pacotes
Além do número do pacote, o Wireshark pode encontrar pacotes por conteúdo. Você pode usar o menu "Editar --> Encontrar Pacote" para pesquisar dentro dos pacotes por um evento de interesse específico. Isso ajuda analistas e administradores a encontrar padrões de intrusão ou rastros de falhas específicos.

Há dois pontos cruciais na busca de pacotes. O primeiro é saber o tipo de entrada. Essa funcionalidade aceita quatro tipos de entrada (filtro de exibição, hexadecimal, string e expressão regular). As buscas por string e expressão regular são os tipos de busca mais comumente usados. As buscas não diferenciam maiúsculas de minúsculas, mas você pode definir a diferenciação clicando no botão de opção.

O segundo ponto é escolher o campo de busca. Você pode realizar buscas nos três painéis (lista de pacotes, detalhes do pacote e bytes do pacote), e é importante saber as informações disponíveis em cada painel para encontrar o evento de interesse. Por exemplo, se você tentar encontrar as informações disponíveis no painel de detalhes do pacote e realizar a busca no painel da lista de pacotes, o Wireshark não as encontrará, mesmo que existam.

<img width="1507" height="766" alt="image" src="https://github.com/user-attachments/assets/8df3d50f-24c2-4ebd-9d55-dc42b2793f12" />

## Marcar Pacotes
Marcar pacotes é outra funcionalidade útil para analistas. Você pode encontrar/apontar para um pacote específico para investigação posterior marcando-o. Isso ajuda os analistas a apontar para um evento de interesse ou exportar pacotes específicos da captura. Você pode usar o menu "Editar" ou o menu "clique com o botão direito" para marcar/desmarcar pacotes.

Os pacotes marcados serão exibidos em preto, independentemente da cor original que representa o tipo de conexão. Observe que as informações dos pacotes marcados são renovadas a cada sessão de arquivo, portanto, os pacotes marcados serão perdidos após o fechamento do arquivo de captura.

<img width="1463" height="425" alt="image" src="https://github.com/user-attachments/assets/3ccea429-69a7-47d9-b034-dfb5e19e6ead" />

## Comentários de Pacotes
Semelhante à marcação de pacotes, os comentários são outro recurso útil para analistas. Você pode adicionar comentários para pacotes específicos que ajudarão na investigação posterior ou lembrar e apontar pontos importantes/suspeitos para outros analistas de camada. Ao contrário da marcação de pacotes, os comentários podem permanecer no arquivo de captura até que o operador os remova.

<img width="1196" height="949" alt="image" src="https://github.com/user-attachments/assets/2f630464-9f6c-48ef-bda9-9a3a4946dd38" />

## Exportar Pacotes
Arquivos de captura podem conter milhares de pacotes em um único arquivo. Como mencionado anteriormente, o Wireshark não é um IDS, portanto, às vezes, é necessário separar pacotes específicos do arquivo e investigar mais a fundo para resolver um incidente. Essa funcionalidade ajuda os analistas a compartilhar apenas os pacotes suspeitos (escopo definido). Dessa forma, informações redundantes não são incluídas no processo de análise. Você pode usar o menu "Arquivo" para exportar pacotes.

O Wireshark pode extrair arquivos transferidos pela rede. Para um analista de segurança, é vital descobrir arquivos compartilhados e salvá-los para investigação posterior. A exportação de objetos está disponível apenas para fluxos de protocolos selecionados (DICOM, HTTP, IMF, SMB e TFTP).

<img width="1415" height="706" alt="image" src="https://github.com/user-attachments/assets/c13c3733-02b6-4955-8b3b-e7458bbd171c" />

<img width="1463" height="621" alt="image" src="https://github.com/user-attachments/assets/919f0936-b4f1-4d1f-bd09-b2044bc41940" />

## Formato de Exibição de Hora

O Wireshark lista os pacotes conforme são capturados, portanto, investigar o fluxo padrão nem sempre é a melhor opção. Por padrão, o Wireshark exibe a hora em "Segundos Desde o Início da Captura". O formato de exibição de hora UTC é usado com mais frequência para uma melhor visualização. Você pode usar o menu "Exibir --> Formato de Exibição de Hora" para alterar o formato de exibição de hora.

## Dica extra

O Wireshark também detecta estados específicos de protocolos para ajudar analistas a identificar facilmente possíveis anomalias e problemas. Observe que estas são apenas sugestões e sempre há a possibilidade de haver falsos positivos/negativos. As Informações de Especialistas podem fornecer um grupo de categorias em três níveis de gravidade diferentes.

Cor e Informação
* Azul = Informações sobre o fluxo de trabalho normal.
* Ciano = Eventos notáveis, como códigos de erro do aplicativo.
* Amarelo = Avisos como códigos de erro incomuns ou declarações de problemas.
* Vermelho = Problemas como pacotes malformados.

<img width="618" height="204" alt="image" src="https://github.com/user-attachments/assets/391f4146-b7a1-4936-bf09-ebcc8eac8eb8" />

Grupo e Informações
Checksum = Erros de soma de verificação.
Deprecated = Uso de protocolo obsoleto.
Comment = Detecção de comentário de pacote.
Malformed = Detecção de pacote malformado.

<img width="142" height="155" alt="image" src="https://github.com/user-attachments/assets/11e524cb-e2a1-444f-a93a-40a2022a5113" />








































