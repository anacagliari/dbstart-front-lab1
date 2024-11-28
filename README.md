# **Laboratório 1 – Configurando Projeto TypeScript e Node**

Este laboratório mostra como criar e configurar um projeto no Visual Studio Code com `TypeScript` e `Node.js`.

---

## **Sumário**

1. [Configuração do Projeto](#1-configuração-do-projeto)
2. [Codificando o Projeto](#2-codificando-o-projeto)
3. [Depurando o Projeto](#3-depurando-o-projeto)

---

## **1. Configuração do Projeto**

### 1.1 Criando o Diretório e Inicializando o Projeto

1. Abra o Visual Studio Code e crie um novo diretório `lab1` dentro do seu repositório GIT criado anteriormente.
2. Abra uma linha de comando dentro do novo diretório. Utilize `CTRL+’` para abrir o terminal embutido do Visual Studio Code.
3. Inicialize o projeto Node com o seguinte comando para criar um arquivo `package.json`:

```bash
npm init -y
```

### 1.2 Instalando o TypeScript

1. Adicione o TypeScript localmente ao novo projeto (dessa forma você pode trabalhar com versões diferentes em cada projeto, sem entrar em conflito com uma instalação global) através do seguinte comando (a opção de instalação indica que o TypeScript é uma dependência de tempo de desenvolvimento que não afetará dependência de tempo de execução/produção do projeto):

```bash
npm install typescript -D
```

ou

```bash
npm install typescript --save-dev
```

2. Observe as alterações efetuadas no arquivo `package.json` e a criação do subdiretório `node_modules` com os pacotes do TypeScript.
3. Verifique se o compilador do `TypeScript` está executando através do comando:

```bash
npx tsc -v
```

4. Acrescente um arquivo `tsconfig.json` com as opções de compilação do `TypeSript` através do comando:

```bash
npx tsc --init
```

5. Abra o arquivo `tsconfig.json` e observe todas as opções disponíveis. Realize as seguintes alterações:

- `"target": ` edite para `"target": "es2022"`
- `"module": ` edite para `"module": "Node16"`
  Descomente as linhas abaixo:
- `"lib": ` edite para: `"lib": ["es2023"]`
- `"moduleResolution"` edite para: `"moduleResolution": "node16"`
- `"sourceMap": true`
- `"outDir": "./"` edite para: `"outDir": "./dist"`
- `"rootDir": "./"` edite para: `"rootDir": "./src"`

6. Crie o subdiretório `src` dentro do projeto
7. Acrescente novas propriedades após a `}` que fecha a propriedade `"compilerOptions"`:

```
"include": ["src/**/*"],
"exclude": ["**/*.spec.ts", "**/*.test.ts"]
```

Observação: alternativamente, utilize um arquivo de configuração base já padronizado para diversos ambientes de desenvolvimento de acordo com a documentação disponível em:

- https://www.typescriptlang.org/docs/handbook/tsconfig-json.html

### Instalando Dependências Adicionais

1. Instale o ambiente de execução `TypeScript` para `Node ts-node` (https://typestrong.org/ts-node/) via o comando:

```bash
npm install ts-node -D
```

ou

```bash
npm install ts-node --save-dev
```

2. Adicione o arquivo de definição de tipos `TypeScript` (arquivos `*.d.ts` serão instalados no diretório `node_modules/@types`) para a biblioteca do `Node` através do seguinte comando:

```bash
npm install @types/node -D
```

ou

```bash
npm install @types/node --save-dev
```

3. Instale o `nodemon` (https://nodemon.io/) para automatizar o processo de compilação a cada alteração de arquivo-fonte via o comando:

```bash
npm install nodemon -D
```

ou

```bash
npm install nodemon --save-dev
```

4. Abra o arquivo `package.json` e localize a seção `scripts`. Iremos alterar essa seção para configurar os comandos de compilação e execução do projeto via `NPM`. O resultado desejado será dois comandos para executar a aplicação `index` em modo de desenvolvimento e de produção:

```bash
npm run dev
```

- Para iniciar a aplicação em modo de desenvolvedor com nodemon habilitado. Nesse ambiente, qualquer alteração no código-fonte da aplicação será automaticamente refletido em uma nova execução.

```bash
npm run start
```

- Para executar a aplicação com o código `TypeScript` do projeto via `ts-node`.

```bash
npm run build
```

- Para compilar a aplicação em código `JavaScript` para posterior distribuição e execução via `node`.

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon src/index.ts",
    "start": "ts-node src/index.ts",
    "build": "tsc"
}
```

5. Crie um novo arquivo `.gitignore` na raiz do diretório do projeto (junto aos arquivos de configuração `*.json` com o seguinte conteúdo. Esse arquivo irá indicar o conteúdo que não deve ser enviado para o repositório Git.)

```bash
node_modules
dist
*.log
```

---

## **2. Codificando o projeto**

1. Crie um arquivo `index.ts` no diretório `src` do projeto. Utilize o seguinte código:

```typescript
let saudacao: string = "Alô, mundo!";
console.log(saudacao);
```

2. Abra um terminal, execute o seguinte comando e observe o resultado, executando o projeto em diferentes modos:

- Modo de desenvolvimento (com nodemon):

```bash
npm run start
```

- Compilação para JavaScript:

```bash
npm run dev
```

3. Execute qualquer alteração no arquivo `index.ts` e verifique que a mesma automaticamente se torna ativa ao salvar. Utilize `CTRL+C` no terminal para sair do `nodemon`.
4. Abra um terminal e execute o comando:

```bash
npm run build
```

6. Observe o resultado dentro do diretório `dist`, dois novos arquivos devem ter sido criados:

- `index.js`
- `index.js.map` que possui o suporte necessário para habilitar a depuração de código via um `debugger`.

---

## **3 Depurando o projeto**

1. Clique no canto esquerdo da linha `console.log` no arquivo `index.ts` para habilitar um ponto de parada.

2. Na janela do Visual Studio Code clique no `ícone de depuração` (o ícone do bug) e selecione `Run and Debug` para iniciar o processo de configuração do depurador.

3. Como não temos um arquivo de configuração de ambiento no Visual Studio Code, será solicitado que se indique o ambiente de depuração adequado. Selecione `Node.js`.

---

**Pronto. Agora estamos depurando a aplicação.**

---

## **Recursos Adicionais**

- [Documentação oficial do TypeScript](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)
- [ts-node](https://typestrong.org/ts-node/)
- [nodemon](https://nodemon.io/)
