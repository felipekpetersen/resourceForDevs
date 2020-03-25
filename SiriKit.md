# Siri Kit
Pedro Farina - https://github.com/PedroFarina

Criar uma integração com a Siri no seu aplicativo pode ser útil para muitas coisas, 
mas a mais encontrada na pesquisa e no meu próprio interesse é a facilidade, 
removendo barreiras para quem usa seu app.

## Pré requisitos
A implementação da Siri está disponível apenas a partir do iOS 12.

## Como funciona
A integração com a siri funciona em três etapas:
1. A primeira é definir o nosso atalho, configurando seus atributos que serão usados.
2. Uma vez que definimos nosso atalho, precisamos informar ao sistema operacional que ele existe, pois nosso atalho poderá ser usado mesmo quando nosso app estiver fechado. Essa ação é chamada de *doação*.
3. Agora que o sistema sabe que o atalho existe, precisamos configurar o app para receber uma chamada do sistema e completar o nosso atalho.

## Como fazer

### NSUserActivity
Na ideia de facilitar o uso do usuário temos dois tipos básicos de usabilidade. O primeiro é com `NSUserActivity`, que é uma integração simples e limitada com o sistema.

Criando uma chave no seu arquivo Info.plist como uma array de strings, pode-se colocar os valores identificadores das suas ações.
**Obs: Estes valores devem ser únicos.**
```xml
<key>NSUserActivityTypes</key>
<array>
	<string>com.PedroFarina.NomeDoAplicativo.Criar-Pedido</string>
</array>
```

Então deve-se criar a atividade pelo construtor `NSUserActivity(activityType: "com.PedroFarina.NomeDoAplicativo.Criar-Pedido")`, e doa-lo ao sistema usando `.persistentIdentifier`.

E no `AppDelegate` implementar a função de continuar uma userActivity:
```swift
func application(_ application: UIApplication, continue userActivity: NSUserActivity, restorationHandler: @escaping ([UIUserActivityRestoring]?) -> Void) -> Bool
```

### Siri Intents
Agora para uma integração mais sofisticada que tenha acesso a mais coisas como processamento em background é necessário usar os Intents da Siri.

Para começar a integração com os Intents da Siri basta adicionar um target a mais no projeto de Intents, criar um arquivo no projeto do tipo `SiriKit Intent Definition File` e configura-lo.

Uma vez que tenhamos o arquivo configurado, temos acesso aos `Intents` criados nesse arquivo, podendo então criar objetos de interação `INInteraction` e doa-las ao sistema.

Uma vez feito isso é necessário criar um `IntentHandler` que deverá lidar com os chamados do mesmo Intent.

**Note que usando Siri Intents não é necessário doar ação para ter acesso a ela pelo Shortcuts**
