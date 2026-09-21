# 78 Semanas para o TCF Canada

Plano de estudo de francês do zero ao TCF Canada em 78 semanas (18 meses), com sete tarefas por
semana — gramática em vídeo, vocabulário, simulado de compreensão, imersão, música, produção
cronometrada e revisão — e progresso marcável. Meta: NCLC 7 nas quatro provas.

Site estático: um único `index.html`, sem build, sem dependências de servidor.

## Arquivos

| Arquivo | Para que serve |
| --- | --- |
| `index.html` | A página inteira: conteúdo, estilos e scripts em um só arquivo |
| `icon.svg` | Ícone da aba e da tela inicial do celular |
| `manifest.json` | Permite instalar a página como app (Adicionar à tela de início) |

## Publicar na Vercel

O projeto não precisa de nenhuma configuração: a Vercel detecta `index.html` na raiz e serve como
site estático. Basta enviar estes arquivos para o repositório do GitHub já importado.

```bash
git init
git add .
git commit -m "Plano de estudo de francês em 78 semanas"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/SEU-REPO.git
git push -u origin main
```

Se o repositório já tiver commits, troque as duas primeiras linhas por `git clone` do repositório e
copie os arquivos para dentro dele.

A cada `git push` na branch `main`, a Vercel reconstrói e publica automaticamente.

### Configuração na Vercel

Se ela pedir para escolher, use:

- **Framework Preset:** Other
- **Build Command:** (vazio)
- **Output Directory:** (vazio, ou `.`)
- **Install Command:** (vazio)

## Sobre o progresso salvo

As marcações são guardadas no `localStorage` do navegador — ficam no aparelho, não em um servidor.
Isso significa:

- O progresso sobrevive a fechar o navegador e a novos deploys.
- Ele **não** sincroniza entre celular e computador automaticamente.
- Para transferir, use os botões **Exportar progresso** / **Importar progresso** no fim da página.
- Limpar os dados do site no navegador apaga o progresso.

Se quiser sincronização real entre aparelhos, o caminho é trocar o `localStorage` por um banco
(Vercel KV, Supabase ou Firebase) e adicionar login. A função que salva está isolada em
`writeLocal()` / `readLocal()` dentro do `index.html`, que são os dois únicos pontos a mudar.

## Editar o conteúdo

O currículo está no array `W`, dentro do `<script>` no fim do `index.html`. Cada semana é um objeto:

```js
{
  w: 1,             // número da semana
  p: "A1",          // fase
  t: "título",      // tema da semana
  g: "…",           // gramática — tarefa de segunda
  y: "akKplmnr01M", // id do vídeo do YouTube que ensina o tema
  yt: "…",          // título mostrado no link do vídeo
  l: "…",           // vocabulário — terça
  yv: "…", yvt: "…",// vídeo de vocabulário (opcional)
  c: "…",           // simulado no formato TCF — quarta
  cp: "ceA1",       // chave da playlist de simulado, no objeto PL
  a: "…",           // imersão em áudio — quinta
  m: "…",           // música — sexta
  pr: "…",          // produção TCF — sábado
  pp: "ee2"         // playlist de modelos de produção (opcional)
}
```

A tarefa de domingo (revisão) é igual em todas as semanas e fica na função `tasksOf()`.

As playlists de simulado TCF ficam no objeto `PL`, no mesmo script. Os campos `c`/`cp` definem
o simulado de quarta e `pr`/`pp` a produção de sábado.

## Créditos das aulas

- Aulas de gramática, vocabulário e pronúncia: [Français avec Pierre](https://www.youtube.com/@Francaisavecpierre) — 137 vídeos, todos verificados.
- Simulados por nível: [TCF CANDA C2](https://www.youtube.com/@TCFCANDAC2-f1e) e [TCF Lab](https://www.youtube.com/@TCFLab).
