# Anúncios em iOS
Pedro Farina - https://github.com/PedroFarina

## Conceito
Hoje em dia existem vários tipos de anúncios mobile:
- Toque para download, que levará o usuário diretamente para uma loja virtual
- Toque para ligação, que levará o usuário para o telefone
- Toque para mensagem, que levará o usuário para suas mensagens
- Textos e banners, que levarão o usuário para uma página qualquer

O mais usado em aplicativos são banners e textos que aparecem de tempos em tempos, podendo mostrar vídeos ou que ficam
numa área da tela. E o provedor desse serviço mais conhecido de anúncios ultimamente é o *Google Ads*.

## Pré requisitos (Google Ads)
- Xcode 10.0+
- iOS 8.0+
- Conta AdMob
- Registrar seu aplicativo no AdMob

## Como fazer

### Setup
Para começar a implementação, é necessário ter em seu projeto as frameworks da *Google*. Podendo incluir no seu projeto
via pods com o comando básico `pod 'Google-Mobile-Ads-SDK'` e depois `pod install --repo-update`. Ou baixar as [frameworks](https://developers.google.com/admob/ios/download)
e adiciona-las no projeto manualmente.

Agora no Info.plist do projeto, será necessário uma chave `GADApplicationIdentifier` com a chave do seu aplicativo cadastrado.

**Para desenvolvimento essa chave deve ser `ca-app-pub-3940256099942544/2934735716` caso contrário sua conta poderá ser suspendida**

***

### Formato de propaganda
Existem quatro formatos atualmente oferecidos pela *Google*:
- Banners, propagandas retangulares que ficam no seu aplicativo
- Interstitial, propagandas de tela cheia que permanecem ativas até o usuário fechar
- Native, propagandas configuráveis para que você como desenvolvedor escolha seu comportamento
- Rewarded, pequenos vídeos ou interações que são comumentes usadas como premios em jogos free-to-play

Todas propagandas terão um ciclo parecido:
1. Delimitar um espaço de uso
2. Carregar uma propaganda
3. Reproduzir

***

### Banners
Para banners, deve-se:

1. Adicionar uma `GADBannerView` com suas constraints
2. Configurar sua `.adUnitID` e sua `.rootViewController`
3. Carregar propagandas
4. Mostrar na `GADBannerView`

Pode-se também obter acesso aos eventos do banner, seguindo o protocolo `GADBannerViewDelegate` para melhor interação
de usuário.

***

### Interstitial
Para interstestials, deve-se:

1. Adicionar uma `GADInterstitial`
2. Carregar uma propaganda
3. Verificar se o interstitial está pronto para mostrar a propaganda
4. Mostrar na `GADInterstitial`
*Obs: `GADInterstitial` são objetos de uso único, portanto uma vez usada, deve-se criar um novo objeto e refazer os passos.*

Semelhante aos banners é possível obter acesso aos eventos do interstitial, seguindo o protocolo `GADInterstitialDelegate`.

***

### Native
As propagandas nativas são mais personalizáveis e portanto mais complexas de implementar. Deve-se:

1. Criar e configurar um `GADAdLoader`
2. Seguir um protocolo `GADUnifiedNativeAdLoaderDelegate` para saber quando as propagandas foram carregadas
3. Mostrar os anúncios em uma `GADUnifiedNativeAdView` configurada de acordo com o seu caso após o carregamento dos mesmos

***

### Rewarded
Para rewardeds deve-se:

1. Criar um `GADRewardedAd`
2. Carregar uma propaganda
3. Verificar se o `GADRewardedAd` está pronto para mostrar essa propaganda
4. Mostrar a propaganda

**Para saber se o usuário recebeu o premio ou não deve-se implementar o protocolo `GADRewardedAdDelegate`**

***
