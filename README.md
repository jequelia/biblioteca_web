# biblioteca
Esse projeto representa uma biblioteca online, onde é permitido cadastar, editar, ver e excluir um livro.

obs: editar e excluir está com bug.

# App.vue
arquivo principal

# components
Existem dois components: 
- um utilizado para construir o forms(Cadastro) - formBiblioteca
- outro utilizado para listar os livros - Biblioteca
# css
Foi utlizando bootstrap-vue para facilitar na resposividade do site.

# comunicação com o back
Foi utilizado a  biblioteca de clientes http axios.

## Passo a passo para a execução

### 1- Executar o build da aplicação vue
> docker build -t nome_image .

### 2- Executar o docker container
> docker run -it -p 8082:8082 --rm --name nome_container nome_image

## Rodando Frontend + Backend

Ao clonar os projetos garanta que ambos estejam na mesma página 
```
/pasta-raiz
--------(frontend)[https://github.com/jequelia/biblioteca_web.git]
--------(backend)[https://github.com/jequelia/biblioteca_api.git]
```
Abra o terminal na pasta raiz e execute o seguinte comando 

> docker-compose -f biblioteca_web/docker-compose.yml -f biblioteca_api/docker-compose.yml config