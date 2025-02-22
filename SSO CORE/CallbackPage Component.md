
**Objetivo:**

- Implementar a lógica de validação de tokens JWT recebidos via callback da autenticação SSO.

```typescript 
import { useEffect } from 'react';
import { useNavigate, useLocation } from 'react-router-dom';

const tokenThresholdLength = 200; // Defina o valor apropriado para o comprimento do token

const CallbackPage = () => {
  const navigate = useNavigate();
  const location = useLocation();

  useEffect(() => {
    const urlParams = new URLSearchParams(location.search);
    const token = urlParams.get('token');
    console.log('Captured token:', token); // Log para depuração

    const decodeToken = (token: string) => {
      try {
        const base64Url = token.split('.')[1];
        const base64 = base64Url.replace(/-/g, '+').replace(/_/g, '/');
        const jsonPayload = decodeURIComponent(atob(base64).split('').map((c) => {
          return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
        }).join(''));
        return JSON.parse(jsonPayload);
      } catch (error) {
        console.error('Erro ao decodificar token:', error);
        return null;
      }
    };

    const handleTokenValidation = async (token: string) => {
      try {
        const response = await fetch('http://localhost:8989/api/auth/validate-jwt', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ token }),
        });

        if (response.ok) {
          const data = await response.json();

          if (data && data.token && data.customerData) {
            localStorage.setItem('token', data.token);
            localStorage.setItem('customerData', JSON.stringify(data.customerData));

            console.log('Token validado e armazenado:', data.token);
            window.location.href = '/select-product';
          } else {
            console.error('Token ou customerData não retornado na resposta:', data);
            navigate('/', { replace: true });
          }
        } else {
          console.error('Erro HTTP ao validar token:', response.status);
          navigate('/', { replace: true });
        }
      } catch (error) {
        console.error('Erro ao validar token:', error);
        navigate('/', { replace: true });
      }
    };

    if (token) {
      if (token.length > tokenThresholdLength) {
        handleTokenValidation(token);
      } else {
        const decodedToken = decodeToken(token);
        console.log('Decoded token:', decodedToken); // Log para depuração

        if (decodedToken && decodedToken.name && decodedToken.userName) {
          const { name, userName } = decodedToken;

          console.log('Token já validado, redirecionando para /select-product');
          localStorage.setItem('token', token);
          localStorage.setItem('customerData', JSON.stringify({ name, userName }));

          window.location.href = '/select-product';
        } else {
          console.error('Dados necessários não encontrados no token decodificado');
          navigate('/', { replace: true });
        }
      }
    } else {
      console.log('oi');
    }
  }, [location.search, navigate]);

  return null; // Este componente não precisa renderizar nada
};

export default CallbackPage;
```

### Notas:

- A função `decodeToken` decodifica o token JWT para extrair informações do payload.
- A função `handleTokenValidation` envia o token ao backend para validação.
- Se a validação for bem-sucedida, o token e os dados do usuário são armazenados no `localStorage`, e o usuário é redirecionado para a página de seleção de produto.
- Se a validação falhar, o usuário é redirecionado para a página incial.