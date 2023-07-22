# Módulos Nativos do Node.js
O Node.js possui vários módulos nativos que oferecem funcionalidades essenciais para o desenvolvimento de aplicativos em JavaScript, permitindo interagir com o sistema operacional, criar servidores web, manipular eventos, realizar resolução de nomes de domínio e muito mais. Abaixo, estão alguns dos principais módulos nativos e suas funcionalidades:

## 1. events
O módulo events permite a criação e manipulação de eventos. Ele fornece uma classe chamada EventEmitter, que é usada para adicionar, remover e emitir eventos personalizados.
````javascript
const { EventEmitter } = require('events');

const eventEmitter = new EventEmitter();

eventEmitter.on('bomdia', (data) => {
  console.log(`Recebi um bom dia de: ${data}`);
});

eventEmitter.emit('bomdia', 'Puc'); // Emitindo o evento 'bomdia' com os dados 'Puc'
````

## 2. http
O módulo http permite a criação de servidores web e interação com requisições e respostas HTTP.
````javascript
cconst http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200; // Código de status OK
  res.setHeader('Content-Type', 'application/json');
  res.end('{ "user": "Fake User", "empresa": "PUC Minas" }');
});

const port = 3000;
server.listen(port, () => {
  console.log(`Servidor rodando em http://localhost:${port}/`);
});
````
## 3. dns
O módulo dns permite realizar resolução de nomes de domínio para endereços IP.
````javascript
const { Resolver } = require('dns');
const resolver = new Resolver();

// Define o servidor DNS a ser utilizado
resolver.setServers(['8.8.8.8']);

// Realiza a tradução de um nome de domínio para um endereço IP
resolver.resolve4('pucminas.br', (err, addresses) => {
  if (err) {
    console.log(`Erro ao traduzir: ${err.message}`);
  } else {
    console.log('Endereço IP: ' + addresses[0]);
  }
});
````
## 4. path
O módulo path permite manipular caminhos de arquivos e diretórios de forma segura, independente do sistema operacional.
````javascript
const path = require('path');

const filePath = '/home/user/documents/report.txt';

console.log('Nome do arquivo:', path.basename(filePath)); // Output: report.txt
console.log('Extensão do arquivo:', path.extname(filePath)); // Output: .txt
console.log('Diretório do arquivo:', path.dirname(filePath)); // Output: /home/user/documents
````

## 5. os
O módulo os fornece informações sobre o sistema operacional, como informações sobre a CPU, memória, entre outros.
````javascript
const os = require('os');

console.log('Plataforma:', os.platform()); // Output: darwin (no macOS)
console.log('Arquitetura:', os.arch()); // Output: x64
console.log('Memória livre (em bytes):', os.freemem());
console.log('Total de memória (em bytes):', os.totalmem());
````
## 6. process
O módulo process fornece informações sobre o processo Node.js em execução e permite interagir com variáveis de ambiente e parâmetros da linha de comando.
````javascript
// Listar todas as variáveis de ambiente
console.log(process.env);

// Acessando argumentos passados na linha de comando
console.log('Argumentos da linha de comando:', process.argv);

// Obtendo informações sobre o processo
console.log('ID do processo:', process.pid);
console.log('Diretório de trabalho atual:', process.cwd());
````
## 7. net
O módulo net permite criar servidores e clientes para comunicação em rede.
````javascript
const net = require('net');

// Criando um servidor TCP
const server = net.createServer((socket) => {
  socket.write('Conexão estabelecida com o servidor!\n');
  socket.end('Encerrando conexão com o servidor!\n');
});

const port = 3000;
server.listen(port, () => {
  console.log(`Servidor TCP rodando na porta ${port}`);
});

// Exemplo de cliente TCP
const client = net.connect({ port: 3000 }, () => {
  console.log('Cliente conectado ao servidor!');
  client.write('Hello, servidor!');
});
client.on('data', (data) => {
  console.log('Mensagem do servidor:', data.toString());
  client.end();
});
````
## 8. url
O módulo url fornece funções para interpretar e manipular strings de URLs.
````javascript
const url = require('url');

const urlString = 'https://www.example.com:8080/path/to/resource?q=search#section';

const parsedUrl = url.parse(urlString, true);

console.log('Protocolo:', parsedUrl.protocol); // Output: https:
console.log('Host:', parsedUrl.host); // Output: www.example.com:8080
console.log('Caminho:', parsedUrl.pathname); // Output: /path/to/resource
console.log('Query:', parsedUrl.query); // Output: { q: 'search' }
console.log('Fragmento:', parsedUrl.hash); // Output: #section
````
## 9. stream
O módulo stream é usado para manipular dados em fluxos, permitindo a leitura e escrita de grandes volumes de dados de forma eficiente.
````javascript
const fs = require('fs');

// Cria um Readable Stream a partir de um arquivo
const readableStream = fs.createReadStream('input.txt', 'utf8');

// Cria um Writable Stream para escrever em um arquivo
const writableStream = fs.createWriteStream('output.txt');

// Pega os dados do Readable Stream e escreve no Writable Stream
readableStream.on('data', (chunk) => {
  writableStream.write(chunk);
});

// Fecha o Writable Stream quando todos os dados forem processados
readableStream.on('end', () => {
  writableStream.end();
});

console.log('Operação de cópia iniciada.');
````
Esses módulos nativos do Node.js são poderosos e essenciais para a criação de aplicativos robustos e eficientes. Com eles, é possível realizar uma ampla variedade de tarefas, desde a criação de servidores web até a manipulação de eventos e resolução de nomes de domínio.
