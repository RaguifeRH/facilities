# Painel Raguife — Indicadores de Restaurante & Higienização

App web (HTML único) com Firebase Auth + Firestore. Perfis: Administrador, Nutricionista e Colaborador. Pesquisa de satisfação anônima via modo tablet (`?kiosk=1`).

## 1. Firebase (uma vez só)

1. **Authentication > Sign-in method**: habilite **E-mail/senha** e também **Anônimo** (usado pelo tablet da pesquisa).
2. **Firestore Database > Regras**: apague o conteúdo e cole o arquivo `firestore.rules` deste repositório. Clique em **Publicar**.
3. (Opcional) **Authentication > Settings > Domínios autorizados**: confirme que o domínio do GitHub Pages (`SEUUSUARIO.github.io`) está na lista — o Firebase costuma pedir isso no primeiro login.

## 2. Publicar no GitHub Pages

1. Crie um repositório (ex: `painel-raguife`) em github.com.
2. Envie os arquivos deste pacote (`index.html`, `firestore.rules`, `README.md`) — pode arrastar pela própria página do GitHub em **Add file > Upload files**.
3. Em **Settings > Pages**: Source = `Deploy from a branch`, Branch = `main` / `/ (root)`. Salvar.
4. Em 1–2 minutos o painel estará em `https://SEUUSUARIO.github.io/painel-raguife/`.

## 3. Primeiro acesso

- Abra o link publicado. Aparecerá o cartão **"Primeiro acesso"** — crie a conta do administrador (nome, e-mail, senha).
- Esse cartão só funciona uma vez; depois disso, contas novas só podem ser criadas por um administrador na aba **Usuários**.

## 4. Tablet da pesquisa

- Aba **Pesquisa Satisfação** → copie o link (`...?kiosk=1`) e deixe aberto no navegador do tablet.
- A tela identifica a refeição pelo horário e as respostas são anônimas.

## 5. EmailJS (cobrança dos checklists)

1. Crie conta em emailjs.com → **Email Services** (conecte seu e-mail) → anote o **Service ID**.
2. Crie **2 templates** (um para checklist ADM, outro para Higiênica) usando as variáveis:
   `{{to_email}}`, `{{to_name}}`, `{{setor}}`, `{{tipo_checklist}}`, `{{link_formulario}}`.
   Em "To email" do template, coloque `{{to_email}}`.
3. Em **Account**, copie a **Public Key**.
4. No painel, logado como admin: **Metas & Config > EmailJS** → cole tudo e salve.
- O disparo automático acontece quando um administrador abre o painel numa **sexta-feira** (uma vez por semana). Também há o botão manual no Dashboard.

## Perfis

| Perfil | Acesso |
|---|---|
| Administrador | Tudo: custos mensais, usuários, metas, EmailJS |
| Nutricionista | Desperdício, compras, dashboard, resultados da pesquisa |
| Colaborador | Apenas os checklists atribuídos (ADM, Higiênica ou ambos) |

Ninguém logado consegue lançar notas na pesquisa de satisfação — ela só existe no modo tablet, e as regras do Firestore impedem edição/exclusão de respostas.
