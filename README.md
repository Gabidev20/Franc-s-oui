# 78 Semanas de Francês

Plano de estudo de francês do zero ao avançado em 78 semanas (18 meses), com sete tarefas por
semana — gramática, vocabulário, vídeo, áudio, música, produção e revisão — e progresso marcável.

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
  w: 1,            // número da semana
  p: "A1",         // fase
  t: "título",     // tema da semana
  g: "…",          // gramática (tarefa de segunda)
  l: "…",          // vocabulário (terça)
  v: "…",          // vídeo (quarta)
  a: "…",          // áudio (quinta)
  m: "…",          // música (sexta)
  pr: "…"          // produção (sábado)
}
```

A tarefa de domingo (revisão) é igual em todas as semanas e fica na função `tasksOf()`.
