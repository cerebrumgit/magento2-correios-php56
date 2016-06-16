![valid XHTML][checkmark]
[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/Red_star_32_32.png "MOZG"
[url-method]: http://www2.correios.com.br/exportafacil/
[requirements]: http://mozgbrasil.github.io/requirements/
[uninstall-mods]: http://devdocs.magento.com/guides/v1.0/install-gde/install/install-cli-uninstall-mods.html
[contact-correios]: http://www2.correios.com.br/sistemas/falecomoscorreios/
[consulta-precos]: http://www2.correios.com.br/sistemas/efi/consulta/precos/default.cfm
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/

# Mozg\Correios

## Sinopse

Integração ao [Correios Exporta Fácil][url-method]

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Recursos

- Definir dimensões para os produtos

- Definir dimensões, peso e valor da Caixa|Embalagem

- Opção para embalar os produtos separadamente ou combinar na mesma Caixa|Embalagem

- Embalagem do produto inteligente, exibe como os produtos serão agrupados e calcula o peso dimensional fazendo o envio fracionado se necessário

- Armazenamento das requisições em Cache

~~- Definir como diferentes combinações de produtos são embalados em conjunto # TODO~~

~~- Atribuir produtos a determinadas caixas (produtos múltiplos podem ser atribuídos à mesma caixa) # TODO~~

## Característica técnica

O módulo foi desenvolvido visando total transparência dos processos executados, para efeito de análise visualize os processos armazenado em log

A extensão permite você definir as dimensões de seus produtos, as dimensões de suas caixas e regras de como empacotar diferentes combinações de produtos em conjunto.

Esta extensão é inteligente o suficiente para escolher quais caixas será utilizado para embalar uma ordem de acordo com itens no carrinho.

A primeira coisa a se levar em consideração no uso do módulo é o gerenciamento de Caixas|Embalagens, como já vem alguns registros pré inseridos certifique se de atualizar os registros para seu projeto.

Certifique se ter cadastrado as devidas dimensões para os produtos.

Para cada pacote é feito um acesso ao WebService onde é passado os devidos parâmetros

O módulo possui armazenamento de cache

Na finalização do pedido é armazenado no histórico do pedido um comentário contendo a discriminação dos pacotes seus itens e a visualização de cada pacote com seus itens em 3D

Sempre confira as informações de frete antes de processar cada pedido, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

## Instalação - Atualização - Desinstalação

Este módulo destina-se a ser instalado usando o composer.

Antes de executar os processos, [clique aqui][requirements] e leia os pré-requisitos e sugestões

--

Para instalar o módulo execute o comando a seguir no terminal do seu servidor

	composer require mozgbrasil/magento2-correios-php56 -vvv && php bin/magento setup:upgrade

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

Para atualizar o módulo execute o comando a seguir no terminal do seu servidor

	composer --version && sudo composer self-update && composer clear-cache && composer update -vvv && composer diagnose && composer show -i && php bin/magento setup:upgrade

--

Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor

	bin/magento module:uninstall --remove-data --backup-code --backup-media --backup-db Mozg_Correios

~~composer remove mozgbrasil/magento2-correios-php56 && composer clear-cache && composer update && php bin/magento setup:upgrade~~

## Como configurar o método de entrega

Antes de configurar o módulo você deve cadastrar o CEP de origem, indo ao backend em:

	STORES -> Configuration -> Sales/Shipping Settings -> Origin

Para configurar o método de entrega, acesse no backend em:

	STORES -> Configuration -> Sales/Shipping Methods -> Correios Exporta Fácil (powered by MOZG)

Você terá os campos a seguir

- **Ativar**

Para "ativar" ou "desativar" o uso do método

- **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

- **Título**

Nome do método que deve ser exibido

- **Serviços**

Selecione os serviços desejado, para selecionar mais de um, segure a tecla "Ctrl" e clique nos serviços

- **Serviço Para Entrega Gratuita**

Quando houver um desconto de frete grátis, esse serviço terá o valor zero

- **Calcular taxa de manuseio**

Podendo ser fixo ou percentual

- **Aplicar Manuseio**

Podendo ser "por ordem" ou "por pacote"

- **Taxa de Manuseio**

Será adicionado o valor ao frete

- **Mostrar método se não aplicável**

Quando configurado como "Não", caso seja retornado alguma opção de frete com erro, não será exibido a opção de frete correspondente nem o motivo do seu erro

- **Debug**

Deve ser armazenado os processos do módulo em var/log/debug.log

- **Enviar para países aplicáveis**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

- **Enviar para países específicos**

Você deve selecionar os países que o método deve ser funcional

Foi mapeado os seguintes países

http://www2.correios.com.br/sistemas/efi/bb/consulta_pais.cfm?reset=true

- **Exibir Prazo de Entrega**

Se será ou não mostrado o prazo de entrega para seu cliente

- **Mensagem que Exibe o Prazo de Entrega**

Se será ou não mostrado o prazo de entrega para seu cliente

- **Adicionar (dias) ao prazo de entrega**

Quantidade de dias que será adicionado ao prazo

## Quais os recursos do módulo

- [✓] Cálculo do frete

## Perguntas mais frequentes "FAQ"

### Como é feito o cálculo de preços

[Clique aqui][consulta-precos] para calcular o preço da encomenda o sistema utiliza a distância origem/destino(CEP), o peso e as dimensões do objeto, aplicando a seguinte fórmula relativa a peso cúbico:

	(Comprimento x Altura x Largura)

O preço adotado pelo sistema será o maior entre o peso cúbico e peso real.

### Como aplicar o Frete Grátis

Na configuração do módulo para o método de entrega é possível definir o "Serviço Para Entrega Gratuita" recurso que deve ser aplicado quando definido a ação de "Frete Grátis" nas "Regras da Promoção"

No Backend do Magento, acesse o menu: Promoções -> Regras de Promoção -> Criar regra -> Crie uma regra e selecione a ação "Frete Grátis"

Dessa forma na exibição do cálculo do frete será exibido para o serviço escolhido o valor zerado

### Dados de contato - Jamef

Para entrar em contato com os [Correios][contact-correios]

## Manual

http://www.correios.com.br/para-sua-empresa/servicos-para-o-seu-contrato/precos-e-prazos/calculador-remoto-de-precos-e-prazos/pdf/EFI_Manual_Implementacao_Calculo_Remoto_de_Precos_e_prazos.pdf

## Contribuintes

Equipe Mozg

## License

[Comercial License] (LICENSE.txt)

## Badges

[![Join the chat at https://gitter.im/mozgbrasil](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mozgbrasil/)
[![Latest Stable Version](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/v/stable)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Total Downloads](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/downloads)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Latest Unstable Version](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/v/unstable)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![License](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/license)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Monthly Downloads](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/d/monthly)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)
[![Daily Downloads](https://poser.pugx.org/mozgbrasil/magento2-correios-php56/d/daily)](https://packagist.org/packages/mozgbrasil/magento2-correios-php56)

:cat2:
