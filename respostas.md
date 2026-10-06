# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome:
Matrícula:
Usuário do GitHub:
Usuário do Docker Hub:

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?

R: Usei o `nginx:alpine` e o tamanho final foi: 93.57 MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.


R:

`/usr/share/nginx/html`

`docker exec -it portal sh`

`ls`
   

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

joaodemutti/agrovale-portal:1.0-26128316
https://hub.docker.com/repository/docker/joaodemutti/agrovale-portal

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

R: Porque é mais seguro.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | curl "http://localhost:7016" | Não foi feito o `COPY` do `index.html` para imagem do container | Não apareceu a página correta | Inserido a linha `COPY ./html ./`, alterado o WORKDIR e pasta local |
| 2 | docker exec manut ls | Os arquivos padrão do nginx não forma removidos | Listagem dos arquivos no diretório html | `RUN rm -rf ./*` |
| 3 | Abrir Dockerfile | Não estava documentado a porta do container | Ausência da porta exposta com o comando `EXPOSE` no Dockerfile | `EXPOSE 80` |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

R: `-p 7042:80` expõe a porta externa 7042 apontando para a porta do container 80, o oposto é feito no `-p 80:7042`. O da direita é do container.

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

R: Porque o localhost é do endereço interno do container e não da rede do docker, já o db é o serviço do docker q serve como o endereço host entre os containers/serviços do compose.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

Por causa de segurança, publicando a porta 3306 está expondo o banco para qualquer um acessar, dá para acessar pelo docker exec ou criar um serviço de acesso admin como o adminer. `docker exec -it db mariadb -u agrovale -p123456`

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

`docker compose up -d`

`docker compose down -v`

o `down -v`, porque apaga os volumes

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
