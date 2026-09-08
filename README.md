# Caderno Temático - [Guia de Estudos de Redes e Mikrotik]

## 1. Contexto e Objetivos
- Explique aqui: Qual tema você escolheu para estudar no NotebookLM e por que escolheu esse assunto? Qual era o seu objetivo?
- R: Escolhi o tema de redes com mikrotik por ser uma ferramenta de redes de fácil acesso e estudo. O objetivo é para entender melhor sobre o Mikrotik e conseguir realizar as configurações.

## 2. Curadoria de Fontes
- Liste de 3 a 5 links, artigos ou materiais que você enviou para o NotebookLM como base de conhecimento.
- R: Coloquei arquivos em PDF que falam sobre redes e mikrotik, a wiki do site oficial da Mikrotik e usei o recurso deep Research que me trouxe 20 excelentes fontes.

## 3. Engenharia de Prompts e "Cicatrizes"
- Quais perguntas você fez para a IA?
- P1: Quais são os passos recomendados na documentação para a primeira configuração segura de um roteador RouterOS?
- P2: Eu tenho dois links de internet. Como faço para configurar os dois dentro do mikrotik usando uma como principal e o outro como secundário? Para facilitar crie um passo a passo simples e utilize os nomes Embratel e Oi para diferenciar os links.
- P3: Como configurar o firewall dentro do mikrotik para manter a segurança e evitar ataques indesejados? Crie um passo a passo de forma simples para conseguir realizar a configuração.

- Teve alguma resposta que veio incompleta ou estranha? Como você ajustou o seu prompt para conseguir a resposta ideal?
- R: Não. Não realizei perguntas de formas basica, procurei diretamente sobre o assunto necessário.

## 4. Miniguia de Estudo (Resultado Final)
- Resumo estruturado do que você aprendeu.
- R: 1. Modelos de Referência (OSI e TCP/IP) e Protocolos Essenciais
Para compreender como a comunicação entre dispositivos funciona, a engenharia de redes utiliza modelos conceituais para dividir o fluxo de dados em camadas lógicas:
Modelos de Rede (OSI e TCP/IP): O Modelo OSI é uma ferramenta didática dividida em 7 camadas (Física, Enlace, Rede, Transporte, Sessão, Apresentação e Aplicação).
Já o Modelo TCP/IP simplifica esse fluxo em 4 camadas (Link, Internet, Transporte e Aplicação), sendo o padrão prático usado para solução de problemas cotidianos.
 - Identificação de Dispositivos (MAC e IP): Cada placa de rede possui um endereço físico e único de fábrica chamado MAC Address (Camada de Enlace/L2).
Para que redes distintas se comuniquem, os dispositivos recebem um endereço lógico chamado IP (Camada de Rede/L3).
O protocolo ARP é o responsável por traduzir e mapear os IPs em seus respectivos MACs na rede local.
 - Protocolos de Suporte: O DNS traduz nomes de domínios em IPs, o DHCP automatiza a entrega de configurações de rede aos clientes, e o protocolo ICMP (base do ping e do traceroute) fornece relatórios de conexão e diagnósticos de erros de rede.
2. Infraestrutura de Camada 2: Bridges e VLANs
A segmentação e a organização das portas físicas de um MikroTik são essenciais para construir redes locais eficientes:
Interface Bridge: No RouterOS, uma Bridge é uma interface virtual que combina múltiplas portas físicas em um único segmento de rede.
Ela faz com que o roteador se comporte como um Switch, permitindo que os dispositivos conectados nessas portas se comuniquem diretamente de forma local.
 - VLANs (Redes Locais Virtuais): Uma VLAN divide virtualmente uma rede local física em múltiplas redes independentes, criando domínios de difusão (broadcast) separados que operam em Camada 2.
 - Bridge VLAN Filtering: No RouterOS v7, a prática moderna recomendada é criar uma única ponte global e ativar a filtragem de VLANs (vlan-filtering=yes).
 - Isso permite que os pacotes locais sejam comutados diretamente pelos chips de switch integrados do MikroTik (chamado de HW Offloading ou aceleração de hardware), poupando significativamente o processador central (CPU) do roteador.
3. Conectividade WAN, DHCP e NAT
Para que um roteador MikroTik estabeleça comunicação externa e distribua internet para a rede interna, três mecanismos precisam trabalhar juntos:
DHCP Client vs. DHCP Server: A interface conectada ao provedor (WAN) geralmente roda um DHCP Client para obter automaticamente o IP de internet e as rotas padrão.
Internamente, o MikroTik roda um DHCP Server nas portas locais (LAN) para atribuir automaticamente endereços IPs aos dispositivos da sua casa ou empresa.
 - IPs Privados e o papel do NAT: A rede interna utiliza faixas de endereçamento reservadas para uso privado (conforme a RFC 1918, como 192.168.0.0/16), que não são roteáveis na internet pública.Para que os computadores locais consigam navegar na internet, o roteador realiza o NAT (Network Address Translation) usando a ação de Masquerade, que traduz de forma transparente os IPs privados locais em um único IP público roteável.
- Rotas Estáticas: Definem o caminho que os pacotes devem seguir. A rota padrão (0.0.0.0/0) serve para direcionar todo o tráfego de destino desconhecido diretamente ao gateway do provedor de internet.
4. Gestão e o Salva-Vidas Administrativo: Safe Mode
O MikroTik RouterOS oferece uma flexibilidade imensa, mas exige cuidados de administração e backup para evitar acidentes operacionais:
- Safe Mode (Modo Seguro): Essa é a ferramenta de proteção mais importante para iniciantes. Ao clicar no botão "Safe Mode" no WinBox ou pressionar [Ctrl]+[X] no terminal, o roteador entra em modo de segurança.
- Se você aplicar qualquer configuração errada de firewall ou roteamento que derrube a sua conexão, o sistema desfaz automaticamente todas as alterações pendentes assim que a sessão cair por timeout, evitando que você fique bloqueado fora do equipamento.
- Tipos de Backups: O MikroTik diferencia as formas de salvar as configurações:
- Arquivos de Backup (.backup): São cópias binárias e criptografadas completas do estado do hardware (incluindo senhas e MACs) e só devem ser restauradas no mesmo aparelho ou em modelos idênticos.
- Scripts de Exportação (.rsc): Gerados pelo comando /export, salvam as configurações ativas em texto claro.São ideais para migrar configurações entre modelos de hardware diferentes.

- Um pequeno glossário (termos técnicos explicados de forma simples).
  R: 
- RouterOS: O sistema operacional que roda nos equipamentos MikroTik.
- Winbox: O programa visual oficial usado para gerenciar e configurar o MikroTik no computador.
- IP / Sub-rede: O endereço único de cada dispositivo e a faixa que define quem está na mesma rede local.
- DHCP: O serviço que entrega endereços IP automaticamente para computadores e celulares conectados.
- NAT: O mecanismo que permite que vários dispositivos da rede local compartilhem um único endereço IP público para navegar na internet.

- Prompts prontos que outras pessoas podem reutilizar para estudar esse tema.
R: 
1 - Explique o passo a passo para configurar uma rede local básica (LAN) no MikroTik, citando o papel da Bridge e do DHCP.
2- Com base nas fontes, quais são as 3 regras de Firewall essenciais para proteger um roteador recém-instalado contra acessos externos indesejados?
3- Crie um quiz com 5 perguntas de múltipla escolha sobre endereçamento IP e RouterOS para testar meus conhecimentos.
