# Home Black Friday A.C.R.E.

Home em `/`, construída com Astro e Lumos. A página inicial do starter foi preservada em `/style-guide`.

## Ativar a captação

1. Confirmar a quinta-feira, horário, condições da oferta, bônus e alcance de “agência completa”.
2. Preparar a entrega por WhatsApp e e-mail, respeitando a preferência informada no cadastro.
3. Publicar a política de privacidade e configurar `PUBLIC_PRIVACY_URL`.
4. O endpoint padrão é `https://acre.apps.n8nitro.com/webhook-test/backfriday-acre`. `PUBLIC_LEAD_ENDPOINT` pode substituí-lo em outro ambiente. Não colocar tokens ou credenciais nessa variável.
5. Fazer novo build após alterar as variáveis. A página é estática.

O endpoint recebe `POST` multipart/FormData com:

- `name`: nome, de 2 a 100 caracteres.
- `email`: endereço de e-mail, até 254 caracteres.
- `whatsapp`: telefone brasileiro com DDD, de 10 ou 11 dígitos, com formatação.
- `profile`: `agency-owner`, `marketing-professional`, `digital-entrepreneur` ou `local-business-owner`.
- `delivery_channel`: `whatsapp`, `email` ou `both` (padrão).
- `campaign`: `black-friday-acre`.

Todos os campos são obrigatórios. O endpoint deve validar os campos no servidor, limitar requisições, proteger contra spam, evitar duplicidades e persistir o cadastro antes de retornar HTTP 2xx. Falhas devem retornar status não-2xx. Se estiver em outro domínio, deve permitir o envio pelo domínio do site via CORS. Um webhook que apenas enfileira uma chamada sem assegurar a persistência não satisfaz esse contrato.

Após resposta HTTP 2xx, o formulário redireciona para `https://pepy.link/q/grupo-aviso-acre`. Em caso de falha, mantém os dados preenchidos e mostra uma mensagem de erro.

Com o endpoint padrão, o botão é liberado quando os campos são válidos. Uma resposta HTTP 2xx do webhook permite o redirecionamento; falhas mantêm os dados preenchidos.

## Antes da publicação

- Substituir `SITE_URL` em `src/consts.ts` pelo domínio confirmado; o valor atual é o domínio do starter.
- Remover `noindex` da home após confirmar as condições comerciais e a integração.
- Trocar a imagem social provisória (logo) por uma composição apropriada para compartilhamento.
- Validar cadastro real, falha de rede, duplicidade, consentimento e entrega pelos canais escolhidos.
- Definir encerramento da captação e atualização da página após a campanha.

## Assets

Logo e fonte copiados do diretório de marca A.C.R.E. fornecido pelo responsável. Metrophobic preserva sua licença OFL em `public/brand/OFL-Metrophobic.txt`.
