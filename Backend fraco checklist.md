## Tarefas de Configuração
- [ ] Consertar o ```redirectUrl```  que está sempre redirecionando para ```http://localhost:5173/callback```
- [ ] Integrar modelo de API novo

 ```
 public function handleProviderCallback()

{

$user = Socialite::driver('microsoft')->user();
  

// Obter o token JWT da resposta

$token = $user->token;

// Configurar o JWT decoder

$config = Configuration::forUnsecuredSigner();

$parsedToken = $config->parser()->parse($token);


// Verificar se é um token sem criptografia

if (!$parsedToken instanceof UnencryptedToken) {

throw new \RuntimeException('Token inválido');

}

  
// Obter os claims desejados

// $name = $parsedToken->claims()->get('name');

// $unique_name = $parsedToken->claims()->get('unique_name');

  
$redirectUrl = 'http://localhost:5173/callback';

$queryParams = http_build_query([

'token' => $token,

]);

// Redirecionar para a URL do React com os dados

return redirect()->away("{$redirectUrl}?{$queryParams}");

}
```


