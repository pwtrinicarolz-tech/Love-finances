<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Love Finances</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,sans-serif;
}

body{
    background:linear-gradient(135deg,#a64dff,#ff66cc);
    min-height:100vh;
    color:white;
}

.login{
    width:350px;
    margin:100px auto;
    background:rgba(255,255,255,0.15);
    backdrop-filter:blur(10px);
    padding:30px;
    border-radius:20px;
    text-align:center;
    box-shadow:0 0 20px rgba(0,0,0,.3);
}

h1{
    margin-bottom:20px;
}

input{
    width:100%;
    padding:12px;
    margin:10px 0;
    border:none;
    border-radius:10px;
}

button{
    background:#ff4da6;
    color:white;
    border:none;
    padding:12px 20px;
    border-radius:12px;
    cursor:pointer;
    margin-top:10px;
}

button:hover{
    background:#ff1a8c;
}

.app{
    display:none;
    padding:20px;
}

.card{
    background:rgba(255,255,255,0.15);
    margin:10px 0;
    padding:20px;
    border-radius:20px;
}

.heart{
    position:fixed;
    font-size:25px;
    animation:float 8s linear infinite;
}

@keyframes float{
    from{
        transform:translateY(100vh);
    }
    to{
        transform:translateY(-100px);
    }
}

table{
    width:100%;
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Love Finances</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,sans-serif;
}

body{
    background:linear-gradient(135deg,#a64dff,#ff66cc);
    min-height:100vh;
    color:white;
}

.login{
    width:350px;
    margin:100px auto;
    background:rgba(255,255,255,0.15);
    backdrop-filter:blur(10px);
    padding:30px;
    border-radius:20px;
    text-align:center;
    box-shadow:0 0 20px rgba(0,0,0,.3);
}

h1{
    margin-bottom:20px;
}

input{
    width:100%;
    padding:12px;
    margin:10px 0;
    border:none;
    border-radius:10px;
}

button{
    background:#ff4da6;
    color:white;
    border:none;
    padding:12px 20px;
    border-radius:12px;
    cursor:pointer;
    margin-top:10px;
}

button:hover{
    background:#ff1a8c;
}

.app{
    display:none;
    padding:20px;
}

.card{
    background:rgba(255,255,255,0.15);
    margin:10px 0;
    padding:20px;
    border-radius:20px;
}

.heart{
    position:fixed;
    font-size:25px;
    animation:float 8s linear infinite;
}

@keyframes float{
    from{
        transform:translateY(100vh);
    }
    to{
        transform:translateY(-100px);
    }
}

table{
    width:100%;
    color:white;
    margin-top:10px;
}

th,td{
    padding:8px;
    text-align:left;
}
</style>
</head>
<body>

<div class="login" id="loginScreen">
    <h1>💜 Love Finances 💜</h1>

    <input type="text" id="user" placeholder="Login">
    <input type="password" id="password" placeholder="Senha">

    <button onclick="login()">Entrar</button>
</div>

<div class="app" id="app">

    <h1>💖 Love Finances 💖</h1>

    <div class="card">
        <h2>Controle Financeiro</h2>

        <input type="text" id="descricao" placeholder="Descrição">

        <input type="number" id="valor" placeholder="Valor">

        <select id="tipo">
            <option value="Receita">Receita</option>
            <option value="Despesa">Despesa</option>
        </select>

        <button onclick="adicionar()">Adicionar</button>

        <h3 id="saldo">Saldo: R$ 0.00</h3>

        <table>
            <thead>
                <tr>
                    <th>Descrição</th>
                    <th>Tipo</th>
                    <th>Valor</th>
                </tr>
            </thead>
            <tbody id="lista"></tbody>
        </table>
    </div>

    <div class="card">
        <h2>📅 Calendário Financeiro</h2>
        <input type="date">
    </div>

    <div class="card">
        <h2>💸 Agendamento Pix</h2>

        <input type="text" id="pixDest" placeholder="Chave Pix">

        <input type="number" id="pixValor" placeholder="Valor">

        <input type="date" id="pixData">

        <button onclick="agendarPix()">Agendar Pix</button>

        <div id="pixLista"></div>
    </div>

    <div class="card">
        <h2>📊 Exportar Excel</h2>

        <button onclick="exportarCSV()">
            Baixar Planilha CSV
        </button>
    </div>

</div>

<script>

const usuarioPadrao = "";
const senhaPadrao = "";

let transacoes = [];
let saldo = 0;

function login(){

    const user =
        document.getElementById("user").value;

    const pass =
        document.getElementById("password").value;

    if(user === usuarioPadrao &&
       pass === senhaPadrao){

        document.getElementById("loginScreen").style.display="none";
        document.getElementById("app").style.display="block";

    }else{
        alert("Login inválido");
    }
}

function adicionar(){

    const descricao =
        document.getElementById("descricao").value;

    const valor =
        parseFloat(document.getElementById("valor").value);

    const tipo =
        document.getElementById("tipo").value;

    if(!descricao || !valor){
        return;
    }

    transacoes.push({
        descricao,
        valor,
        tipo
    });

    if(tipo==="Receita"){
        saldo += valor;
    }else{
        saldo -= valor;
    }

    atualizarTabela();
}

function atualizarTabela(){

    const lista =
        document.getElementById("lista");

    lista.innerHTML="";

    transacoes.forEach(t=>{

        lista.innerHTML += `
        <tr>
            <td>${t.descricao}</td>
            <td>${t.tipo}</td>
            <td>R$ ${t.valor}</td>
        </tr>`;
    });

    document.getElementById("saldo")
    .innerText =
    `Saldo: R$ ${saldo.toFixed(2)}`;
}

function exportarCSV(){

    let csv =
    "Descrição,Tipo,Valor\n";

    transacoes.forEach(t=>{
        csv +=
        `${t.descricao},${t.tipo},${t.valor}\n`;
    });

    const blob =
    new Blob([csv],
    {type:"text/csv"});

    const url =
    URL.createObjectURL(blob);

    const a =
    document.createElement("a");

    a.href=url;
    a.download="love-finances.csv";
    a.click();
}

function agendarPix(){

    const chave =
    document.getElementById("pixDest").value;

    const valor =
    document.getElementById("pixValor").value;

    const data =
    document.getElementById("pixData").value;

    document.getElementById("pixLista").innerHTML +=
    `<p>💖 Pix agendado para ${data}
    | Chave: ${chave}
    | Valor: R$ ${valor}</p>`;
}

for(let i=0;i<25;i++){

    const heart =
    document.createElement("div");

    heart.className="heart";

    heart.innerHTML="💖";

    heart.style.left=
    Math.random()*100+"vw";

    heart.style.animationDuration=
    (5+Math.random()*10)+"s";

    document.body.appendChild(heart);
}

</script>

</body>
</html>    color:white;
    margin-top:10px;
}

th,td{
    padding:8px;
    text-align:left;
}
</style>
</head>
<body>

<div class="login" id="loginScreen">
    <h1>💜 Love Finances 💜</h1>

    <input type="text" id="user" placeholder="Login">
    <input type="password" id="password" placeholder="Senha">

    <button onclick="login()">Entrar</button>
</div>

<div class="app" id="app">

    <h1>💖 Love Finances 💖</h1>

    <div class="card">
        <h2>Controle Financeiro</h2>

        <input type="text" id="descricao" placeholder="Descrição">

        <input type="number" id="valor" placeholder="Valor">

        <select id="tipo">
            <option value="Receita">Receita</option>
            <option value="Despesa">Despesa</option>
        </select>

        <button onclick="adicionar()">Adicionar</button>

        <h3 id="saldo">Saldo: R$ 0.00</h3>

        <table>
            <thead>
                <tr>
                    <th>Descrição</th>
                    <th>Tipo</th>
                    <th>Valor</th>
                </tr>
            </thead>
            <tbody id="lista"></tbody>
        </table>
    </div>

    <div class="card">
        <h2>📅 Calendário Financeiro</h2>
        <input type="date">
    </div>

    <div class="card">
        <h2>💸 Agendamento Pix</h2>

        <input type="text" id="pixDest" placeholder="Chave Pix">

        <input type="number" id="pixValor" placeholder="Valor">

        <input type="date" id="pixData">

        <button onclick="agendarPix()">Agendar Pix</button>

        <div id="pixLista"></div>
    </div>

    <div class="card">
        <h2>📊 Exportar Excel</h2>

        <button onclick="exportarCSV()">
            Baixar Planilha CSV
        </button>
    </div>

</div>

<script>

const usuarioPadrao = "love";
const senhaPadrao = "123456";

let transacoes = [];
let saldo = 0;

function login(){

    const user =
        document.getElementById("user").value;

    const pass =
        document.getElementById("password").value;

    if(user === usuarioPadrao &&
       pass === senhaPadrao){

        document.getElementById("loginScreen").style.display="none";
        document.getElementById("app").style.display="block";

    }else{
        alert("Login inválido");
    }
}

function adicionar(){

    const descricao =
