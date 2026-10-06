# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Matheus Raiano Santos
Matrícula: 26174983
Usuário do GitHub: matheusraiano
Usuário do Docker Hub: matheusraiano

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
R: nginx:latest - 34MB

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.
R: /usr/share/nginx/html . - ls -l /usr/share/nginx/html

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
R: matheusraiano/viaserra-portal:1.0-26174983 - https://hub.docker.com/r/matheusraiano/viaserra-portal

4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
R: docker build -f portal/Dockerfile -t matheusraiano/viaserra-portal:1.0-26174983 . - docker push matheusraiano/viaserra-portal:1.0-26174983

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.
R: 

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | CMD ["nginx"] | não entendi direito, mas não rodava | retirei completamente |
| 2 | /usr/share/nginx | não ia pro index.html | /usr/share/nginx/html |
| 3 | pagina/ | não ia pra página certa | site/ |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
R: O segundo número é sempre a porta do container. Portanto, -p 7042:80 mapeia a porta 7042 do seu PC para a porta 80 do container, enquanto inverter para -p 80:7042 tenta usar a porta 80 do seu PC, o que geralmente gera erro por já estar ocupada.

## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.
R: docker run -d --name portal -p 8083:80 --restart unless-stopped matheusraiano/viaserra-portal:1.0-26174983 - docker run -d --name manutencao -p 7083:80 --restart unless-stopped manutencao:26174983

8. Qual comando derruba os dois containers de uma vez?
R: docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador:

```
================================================================
 Verificador · Avaliação Prática de Docker · Turma C
================================================================
 Matrícula 26174983 · portal 8083 · manutenção 7083

A. Arquivos e Git
[FALHA] A1 portal/Dockerfile segue os requisitos
         -> imagem base sem tag fixa (ou :latest).
[ OK ] A2 .env fora do Git e .env.example versionado
[FALHA] A3 4+ commits e remoto no GitHub (encontrados: 2)
         -> faça um commit por parte e configure o origin
[ OK ] A4 imagem matheusraiano/viaserra-portal:1.0-26174983 pública no Docker Hub

B. docker compose
[ OK ] B1 serviços portal e manutencao em execução
[ OK ] B2 portal roda a imagem publicada
[ OK ] B3 portas: portal em 8083 e manutenção em 7083

C. Conteúdo
[ OK ] C1 portal mostra seu nome e sua matrícula
[ OK ] C2 página de manutenção servindo o aviso "Voltamos em breve"

================================================================
 Resultado: 7/9 verificações
 Ainda há falhas. Corrija e rode de novo.
================================================================
```
