# MUVESKILL BH no GitHub Pages

O GitHub Pages hospeda a interface estática. O login, os perfis e as fotos ficam no Supabase. Para este piloto, o plano gratuito é suficiente.

## 1. Criar o projeto Supabase

1. Crie um projeto em [supabase.com](https://supabase.com/).
2. Abra **SQL Editor**, cole o conteúdo de `supabase-schema.sql` e execute.
3. Em **Authentication → Providers**, deixe o provedor **Email** ativo.
4. Em **Authentication → URL Configuration**, cadastre a URL final do GitHub Pages, por exemplo:

   `https://SEU_USUARIO.github.io/SEU_REPOSITORIO/`

   Use a mesma URL em **Site URL** e em **Redirect URLs**.

## 2. Conectar o front-end

Abra **Project Settings → API** e copie somente:

- **Project URL**
- **Publishable key** (ou a chave legada **anon public**)

Cole os dois valores em `supabase-config.js`:

```js
window.MUVESKILL_SUPABASE_CONFIG = {
  url: 'https://seu-projeto.supabase.co',
  anonKey: 'sua-chave-publica'
};
```

Nunca coloque a chave `service_role` ou qualquer chave secreta no GitHub. A chave pública foi feita para ser usada no navegador; as regras RLS do schema protegem os dados.

## 3. Publicar no GitHub

Envie para o repositório estes arquivos:

- `index.html`
- `supabase-config.js`
- `supabase-schema.sql` (documentação/schema)

Depois, em **Settings → Pages**, escolha a branch principal e a pasta raiz (`/root`). A interface abre com `index.html`.

## O que já está preparado

- Entrar e criar conta com e-mail e senha.
- Perfil individual vinculado ao usuário autenticado.
- Trocar foto de perfil, foto de capa e adicionar fotos à galeria.
- Destaques continuam limitados a seis fotos.
- Upload protegido na pasta do próprio usuário, com limite de 8 MB por imagem.
- Perfis e oportunidades podem ser sincronizados com o Supabase quando o usuário está conectado.
- Estrutura SQL para perfis, oportunidades e candidaturas.

Sem preencher `supabase-config.js`, o protótipo continua navegável em modo de demonstração; textos podem ser testados localmente, mas login e publicação de fotos ficam desativados.
