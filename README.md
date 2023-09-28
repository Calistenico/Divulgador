<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Divulgador de Rede Social</title>
    <!-- Inclua o link para a fonte Pacifico -->
    <link href="https://fonts.googleapis.com/css?family=Pacifico&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-firestore.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-auth.js"></script>
    <style>
        /* Estilos para o aplicativo */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-image: url('https://neilpatel.com/wp-content/uploads/2019/07/ilustracao-representando-smartphone-com-post-do-ap.jpeg');
            background-size: cover;
            background-repeat: no-repeat;
        }

        header {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 10px;
        }

        /* Estilos para o título com a fonte Pacifico */
        header h1 {
            margin: 0;
            font-family: 'Pacifico', cursive;
        }

        button {
            background-color: #f33207;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        main {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        /* Estilos para a caixa de compartilhamento de link do perfil */
        .content-box {
            width: 100%;
            max-width: 400px;
            background-color: rgba(94, 89, 89, 0.9);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        .content-box h2 {
            text-align: center;
            margin-bottom: 10px;
            background-color: rgba(117, 113, 113, 0.815);
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        .content-box p {
            font-size: 16px;
            text-align: center;
            margin-bottom: 20px;
        }

        .copy {
            background-color: #332f2fe1;
            color: white;
            padding: 10px;
            border-radius: 5px;
            text-align: center;
            margin-top: 11px;
        }

        .copy a {
            color: white;
            text-decoration: none;
        }

        /* Estilos para o formulário de compartilhamento de link */
        #postForm label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        #postForm input[type="text"] {
            width: 100%;
            padding: 5px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        #postForm button[type="submit"] {
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        /* Estilos para a carteira de pontos no canto da página */
        #points-wallet {
            position: fixed;
            top: 20px;
            right: 20px;
            width: 120px;
            background-color: rgba(168, 168, 168, 0.9);
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #points-wallet h2 {
            font-size: 16px;
            margin: 0;
        }

        #points-wallet p {
            font-size: 18px;
            margin: 0;
        }

        /* Estilos para a seção de compartilhamento de feeds e fotos */
        #shared-content-box {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #shared-content-box h2 {
            text-align: center;
            margin-bottom: 20px;
        }

        /* Estilos para os botões de acesso ao conteúdo compartilhado */
        .postagem {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 10px;
        }

        .postagem button {
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        .postagem button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
        footer {
            bottom: 0;
            left: 0;
            right: 0;
            text-align: center;
            background-color: #292828bd;
            color: white;
            padding: 7px;
        }
    </style>
</head>
<body>
    
    <header>
        <h1>Divulgador De Rede Social</h1>
    </header>
    
    <main>
        <section id="entry-form" class="content-box">
            <h2>Informe seu Nome e Email</h2>
            <form id="entryForm">
                <label for="nome">Nome:</label>
                <input type="text" id="nome" required>
                
                <label for="email">Email:</label>
                <input type="email" id="email" required>
                
                <button type="submit">Entrar</button>
            </form>
        </section>
        
        <section id="points-wallet">
            <h2>Carteira de Pontos</h2>
            <p id="user-points">Pontos: 20</p>
        </section>
        <section id="profile-link-box" class="content-box">
            <p class="copy">
                Aqui está o melhor: ganhe pontos a cada ação! 😲<br>
                1 ponto por cada curtida 💖<br>
                1 ponto por cada comentário 🗨️<br>
                E o que você pode fazer com esses pontos? 🤔<br>
                <br>
                Quando você acumular 2 pontos, você pode impulsionar sua própria publicação para alcançar mais pessoas e obter ainda mais curtidas, comentários e compartilhamentos! 🚀🔝<br>
                <br>
                O aplicativo perfeito para aqueles que buscam conexões autênticas e crescimento na rede social! 🤝<br>
                <br>
                Comece a acumular pontos enquanto sua presença na rede social decola! 📱💥<br>
                <br>
                #Compartilhar. #Curtir. #Comentar. #Crescer. 📈💫
            </p>
            
            <h2>Compartilhe seus Feeds, Stories e Fotos</h2>
            <p>Divulgue seu perfil organicamente com potencial de tráfego pago.</p>
            <form id="postForm">
                <label for="linkPostagem">Link do seu Perfil:</label>
                <input type="text" id="linkPostagem" required>
                <button type="submit">Compartilhar</button>
            </form>
            <p class="copy">Cada compartilhamento custa 2 pontos.</p>
        </section>

        <section id="shared-content-box">
            <h2>Ganhe Pontos Curtindo e Comentando Feeds, Stories e Fotos</h2>
            <div id="sharedContent">
                <!-- Aqui serão exibidos os links compartilhados -->
            </div>
        </section>
    </main>

    <footer>
        &copy; 2023 Criado com o propósito de uma divulgação orgânica de perfil de Rede Social
    </footer>

    <script>
        // For Firebase JS SDK v7.20.0 and later, measurementId is optional
       <!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Divulgador de Rede Social</title>
    <!-- Inclua o link para a fonte Pacifico -->
    <link href="https://fonts.googleapis.com/css?family=Pacifico&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-firestore.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-auth.js"></script>
    <style>
        /* Estilos para o aplicativo */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-image: url('https://neilpatel.com/wp-content/uploads/2019/07/ilustracao-representando-smartphone-com-post-do-ap.jpeg');
            background-size: cover;
            background-repeat: no-repeat;
        }

        header {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 10px;
        }

        /* Estilos para o título com a fonte Pacifico */
        header h1 {
            margin: 0;
            font-family: 'Pacifico', cursive;
        }

        button {
            background-color: #f33207;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        main {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        /* Estilos para a caixa de compartilhamento de link do perfil */
        .content-box {
            width: 100%;
            max-width: 400px;
            background-color: rgba(94, 89, 89, 0.9);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        .content-box h2 {
            text-align: center;
            margin-bottom: 10px;
            background-color: rgba(117, 113, 113, 0.815);
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        .content-box p {
            font-size: 16px;
            text-align: center;
            margin-bottom: 20px;
        }

        .copy {
            background-color: #332f2fe1;
            color: white;
            padding: 10px;
            border-radius: 5px;
            text-align: center;
            margin-top: 11px;
        }

        .copy a {
            color: white;
            text-decoration: none;
        }

        /* Estilos para o formulário de compartilhamento de link */
        #postForm label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        #postForm input[type="text"] {
            width: 100%;
            padding: 5px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        #postForm button[type="submit"] {
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        /* Estilos para a carteira de pontos no canto da página */
        #points-wallet {
            position: fixed;
            top: 20px;
            right: 20px;
            width: 120px;
            background-color: rgba(168, 168, 168, 0.9);
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #points-wallet h2 {
            font-size: 16px;
            margin: 0;
        }

        #points-wallet p {
            font-size: 18px;
            margin: 0;
        }

        /* Estilos para a seção de compartilhamento de feeds e fotos */
        #shared-content-box {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #shared-content-box h2 {
            text-align: center;
            margin-bottom: 20px;
        }

        /* Estilos para os botões de acesso ao conteúdo compartilhado */
        .postagem {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 10px;
        }

        .postagem button {
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        .postagem button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
        footer {
            bottom: 0;
            left: 0;
            right: 0;
            text-align: center;
            background-color: #292828bd;
            color: white;
            padding: 7px;
        }
    </style>
</head>
<body>
    
    <header>
        <h1>Divulgador De Rede Social</h1>
    </header>
    
    <main>
        <section id="entry-form" class="content-box">
            <h2>Informe seu Nome e Email</h2>
            <form id="entryForm">
                <label for="nome">Nome:</label>
                <input type="text" id="nome" required>
                
                <label for="email">Email:</label>
                <input type="email" id="email" required>
                
                <button type="submit">Entrar</button>
            </form>
        </section>
        
        <section id="points-wallet">
            <h2>Carteira de Pontos</h2>
            <p id="user-points">Pontos: 20</p>
        </section>
        <section id="profile-link-box" class="content-box">
            <p class="copy">
                Aqui está o melhor: ganhe pontos a cada ação! 😲<br>
                1 ponto por cada curtida 💖<br>
                1 ponto por cada comentário 🗨️<br>
                E o que você pode fazer com esses pontos? 🤔<br>
                <br>
                Quando você acumular 2 pontos, você pode impulsionar sua própria publicação para alcançar mais pessoas e obter ainda mais curtidas, comentários e compartilhamentos! 🚀🔝<br>
                <br>
                O aplicativo perfeito para aqueles que buscam conexões autênticas e crescimento na rede social! 🤝<br>
                <br>
                Comece a acumular pontos enquanto sua presença na rede social decola! 📱💥<br>
                <br>
                #Compartilhar. #Curtir. #Comentar. #Crescer. 📈💫
            </p>
            
            <h2>Compartilhe seus Feeds, Stories e Fotos</h2>
            <p>Divulgue seu perfil organicamente com potencial de tráfego pago.</p>
            <form id="postForm">
                <label for="linkPostagem">Link do seu Perfil:</label>
                <input type="text" id="linkPostagem" required>
                <button type="submit">Compartilhar</button>
            </form>
            <p class="copy">Cada compartilhamento custa 2 pontos.</p>
        </section>

        <section id="shared-content-box">
            <h2>Ganhe Pontos Curtindo e Comentando Feeds, Stories e Fotos</h2>
            <div id="sharedContent">
                <!-- Aqui serão exibidos os links compartilhados -->
            </div>
        </section>
    </main>

    <footer>
        &copy; 2023 Criado com o propósito de uma divulgação orgânica de perfil de Rede Social
    </footer>

    <script>
        // For Firebase JS SDK v7.20.0 and later, measurementId is optional
        const firebaseConfig = {
            apiKey: "SUA_API_KEY",
            authDomain: "SEU_DOMÍNIO.firebaseapp.com",
            databaseURL: "https://SEU_DOMÍNIO.firebaseio.com",
            projectId: "SEU_PROJETO_ID",
            storageBucket: "SEU_DOMÍNIO.appspot.com",
            messagingSenderId: "SEU_SENDER_ID",
            appId: "SEU_APP_ID",
            measurementId: "SEU_MEASUREMENT_ID"
        };

        // Inicialize o Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        // ...

        // Função para processar o formulário de entrada
        const entryForm = document.getElementById('entryForm');
        entryForm.addEventListener('submit', function (e) {
            e.preventDefault(); // Impede o envio padrão do formulário
        
            const nome = document.getElementById('nome').value;
            const email = document.getElementById('email').value;
        
            // Verifica se o nome e o email foram fornecidos
            if (nome && email) {
                // Adicione o nome e o email do usuário ao Firestore
                db.collection("usuarios").add({
                    nome: nome,
                    email: email,
                }).then(function (docRef) {
                    console.log("Usuário registrado com ID: ", docRef.id);
                    // Redirecione o usuário para a página principal após o registro
                    window.location.href = "invençao.html"; // Substitua "index.html" pelo nome do arquivo da sua página principal
                }).catch(function (error) {
                    console.error("Erro ao registrar usuário: ", error);
                });
            } else {
                alert('Por favor, preencha todos os campos.');
            }
        });
    </script>
</body>
</html>


        // Inicialize o Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        // ...

        // Função para processar o formulário de entrada
        const entryForm = document.getElementById('entryForm');
        entryForm.addEventListener('submit', function (e) {
            e.preventDefault(); // Impede o envio padrão do formulário
        
            const nome = document.getElementById('nome').value;
            const email = document.getElementById('email').value;
        
            // Verifica se o nome e o email foram fornecidos
            if (nome && email) {
                // Adicione o nome e o email do usuário ao Firestore
                db.collection("usuarios").add({
                    nome: nome,
                    email: email,
                }).then(function (docRef) {
                    console.log("Usuário registrado com ID: ", docRef.id);
                    // Redirecione o usuário para a página principal após o registro
                    window.location.href = "invençao.html"; // Substitua "index.html" pelo nome do arquivo da sua página principal
                }).catch(function (error) {
                    console.error("Erro ao registrar usuário: ", error);
                });
            } else {
                alert('Por favor, preencha todos os campos.');
            }
        });
    </script>
</body>
