Documentação - Criador de Receitas com Hugging Face e JavaScript
Visão Geral
Este projeto é um Criador de Receitas que utiliza o modelo de linguagem GPT-2 da Hugging Face para gerar receitas baseadas nos ingredientes fornecidos pelo usuário. A aplicação possui uma interface simples onde o usuário pode inserir os ingredientes disponíveis, e o modelo irá gerar uma receita com base nesses ingredientes.

A aplicação é construída com as seguintes tecnologias:

JavaScript para a lógica de interação e comunicação com a API.
HTML para a estruturação da interface do usuário.
CSS para estilização da página.
Axios para fazer requisições HTTP para a API do Hugging Face.
Hugging Face API para gerar textos (receitas) com base no modelo GPT-2.
Funcionalidade
A aplicação possui um formulário simples que solicita os ingredientes disponíveis para gerar uma receita. Ao submeter o formulário, a aplicação envia uma solicitação para um servidor (ou diretamente para a API do Hugging Face) e recebe uma receita gerada pelo modelo GPT-2. Essa receita é exibida na página para o usuário.

Fluxo de funcionamento:
O usuário insere os ingredientes no campo de texto.
Ao submeter o formulário, o JavaScript envia a solicitação para a API do Hugging Face (via Axios) com os ingredientes como entrada.
A API responde com uma receita gerada pelo modelo GPT-2.
O texto gerado é exibido na interface para o usuário.
Tecnologias Usadas
Hugging Face API: Utiliza a API de inferência da Hugging Face para chamar o modelo GPT-2 e gerar texto com base nos ingredientes fornecidos.
JavaScript (Axios): Responsável por fazer a comunicação entre o frontend e a API do Hugging Face.
HTML: Utilizado para estruturar a interface do usuário.
CSS: Usado para estilizar a página da web.
Fetch API: Para enviar dados ao backend e receber a resposta da receita.
Como Instalar e Usar
Requisitos
Node.js (recomendado versão 16.x ou superior)
NPM (gerenciador de pacotes do Node)
Conta no Hugging Face: Para obter a chave da API necessária.
Passo a Passo
Clone ou Baixe o Repositório

Clone este repositório ou baixe o código-fonte:
git clone https://github.com/usuário/projeto-criador-receitas.git
Instalar Dependências

Navegue até o diretório do projeto e instale as dependências necessárias:

bash
Copiar
cd projeto-criador-receitas
npm install
Isso instalará o Axios, que é a biblioteca usada para fazer as requisições HTTP à API do Hugging Face.

Configuração do Hugging Face API Key

Você precisará de um token de autenticação da Hugging Face API para poder usar o modelo GPT-2. Para isso:

Crie uma conta em Hugging Face.
Vá até a Página de Tokens e gere um novo token.
Substitua a variável HF_API_KEY no código com o token gerado.
Configuração do Servidor (opcional)

Caso queira rodar o código localmente com um servidor para testar a funcionalidade completa, você pode configurar um servidor simples com Node.js:

Instale o Express:
npm install express

Crie um arquivo server.js com o seguinte conteúdo:
const express = require('express');
const axios = require('axios');
const app = express();
const port = 3000;

app.use(express.json());
app.use(express.static('public')); // Para servir os arquivos estáticos (HTML, CSS, JS)

const HF_API_KEY = 'YOUR_HUGGING_FACE_API_KEY';
const HF_API_URL = 'https://api-inference.huggingface.co/models/gpt2';

app.post('/gerar-receita', async (req, res) => {
    try {
        const { ingredientes } = req.body;
        const response = await axios.post(HF_API_URL, {
            inputs: ingredientes,
            parameters: { max_length: 100, temperature: 0.7, do_sample: true }
        }, {
            headers: {
                'Authorization': `Bearer ${HF_API_KEY}`,
                'Content-Type': 'application/json'
            }
        });
        res.json({ receita: response.data[0].generated_text });
    } catch (error) {
        res.status(500).json({ message: 'Erro ao gerar a receita' });
    }
});

app.listen(port, () => {
    console.log(`Servidor rodando em http://localhost:${port}`);
});
Substitua YOUR_HUGGING_FACE_API_KEY pela chave da API do Hugging Face.

Executar a Aplicação

Se estiver usando o servidor local:

bash
Copiar
node server.js
Acesse a aplicação no navegador através de http://localhost:3000.

Usar a Aplicação

Abra o navegador e vá até a URL onde a aplicação está rodando (por exemplo, http://localhost:3000).
Digite os ingredientes disponíveis no campo de entrada (por exemplo, "ovos, farinha, leite").
Clique em "Gerar Receita" para ver a receita gerada pelo modelo GPT-2.
Exemplo de Resposta da API
A resposta da API será uma receita gerada com base nos ingredientes fornecidos. Por exemplo:

Entrada:

makefile
Copiar
Ingredientes: ovos, farinha, leite
Saída:

markdown
Copiar
Receita: Bolo Simples de Ovos

Ingredientes:
- 2 ovos
- 1 xícara de farinha de trigo
- 1/2 xícara de leite
- 1/2 xícara de açúcar
- 1 colher de chá de fermento em pó

Modo de preparo:
1. Bata os ovos com o açúcar até formar um creme claro.
2. Adicione a farinha e o leite, mexendo até a massa ficar homogênea.
3. Acrescente o fermento e misture delicadamente.
4. Despeje a massa em uma forma untada e leve ao forno pré-aquecido a 180°C por cerca de 30 minutos.
5. Deixe esfriar antes de servir.

Licença
Este projeto está licenciado sob a MIT License.
