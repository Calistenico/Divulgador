<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Divulgador de Rede Social</title>
    <link href="https://fonts.googleapis.com/css?family=Pacifico&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-auth.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-database.js"></script>
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
        .link-button {
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
            margin: 5px;
        }

        .link-button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }

        /* Estilos para o formulário de login */
        #loginForm {
            width: 100%;
            max-width: 400px;
            background-color: rgba(94, 89, 89, 0.9);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #loginForm label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        #loginForm input[type="text"], #loginForm input[type="password"] {
            width: 100%;
            padding: 5px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        #loginForm button[type="submit"] {
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }

        #loginForm p {
            text-align: center;
            margin-top: 10px;
        }

        /* Estilos para os botões de link com imagem */
        .link-button img {
            max-width: 100%;
            height: auto;
            display: block;
            margin: 0 auto 5px;
        }
    </style>
</head>
<body>
    
    <header>
        <h1>Divulgador De Rede Social</h1>
        <div id="user-info">
            <span id="user-email"></span>
            <button id="logoutButton">Sair</button>
        </div>
    </header>
    
    <main>
        <section id="points-wallet">
            <h2>Carteira de Pontos</h2>
            <p id="user-points">Pontos: 10</p>
        </section>

        <section id="loginForm" class="content-box">
            <h2>Login</h2>
            <form id="loginUserForm">
                <label for="email">Email:</label>
                <input type="text" id="loginEmail" required>
                <label for="password">Senha:</label>
                <input type="password" id="loginPassword" required>
                <button type="submit">Entrar</button>
                <p>Ainda não tem uma conta? <a href="#" id="createAccountLink">Crie uma conta</a></p>
            </form>
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
            <div id="sharedContent" class="shared-links">
                <!-- Aqui serão exibidos os links compartilhados como botões -->
            </div>
        </section>
    </main>

    <footer>
        &copy; 2023 Criado com o propósito de uma divulgação orgânica de perfil de Rede Social
    </footer>

    <script>
        // For Firebase JS SDK v7.20.0 and later, measurementId is optional
      const firebaseConfig = {
      apiKey: "AIzaSyDj37BRgxhz60iKLjeEMNeKbgIg85Y2Gz8",
      authDomain: "divulgador-c580f.firebaseapp.com",
      databaseURL: "https://divulgador-c580f-default-rtdb.firebaseio.com",
      projectId: "divulgador-c580f",
      storageBucket: "divulgador-c580f.appspot.com",
      messagingSenderId: "633655897119",
      appId: "1:633655897119:web:01af240d759bec0e18b92a",
      measurementId: "G-5K9YGDBFNK"
        };

        // Inicialize o Firebase
        firebase.initializeApp(firebaseConfig);

        // Referência para o banco de dados
        const database = firebase.database();

        function updateSharedFeed() {
            var sharedContentElement = document.getElementById('sharedContent');

            // Obtém os links compartilhados do banco de dados
            var sharedLinksRef = database.ref('sharedLinks');
            sharedLinksRef.once('value').then(function(snapshot) {
                var links = snapshot.val();
                if (links) {
                    sharedContentElement.innerHTML = ''; // Limpa o conteúdo existente

                    var linksArray = Object.values(links);

                    // Divide os links em grupos de 8
                    for (var i = 0; i < linksArray.length; i += 8) {
                        var linkGroup = linksArray.slice(i, i + 8);
                        var linkGroupDiv = document.createElement('div');

                        // Cria botões para os links no grupo
                        linkGroup.forEach(function(linkObj) {
                            var linkButton = document.createElement('button');
                            var linkText = linkObj.link;
                            var imageUrl = linkObj.imageUrl; // URL da imagem
                            var imgElement = document.createElement('img'); // Elemento de imagem

                            if (imageUrl) {
                                imgElement.src = imageUrl; // Define a fonte da imagem
                                imgElement.alt = linkText; // Adicione um atributo alt para acessibilidade
                                linkButton.appendChild(imgElement); // Adicione a imagem ao botão
                            } else {
                                linkButton.textContent = linkText; // Se não houver imagem, use o texto do link
                            }

                            linkButton.className = 'link-button';
                            linkGroupDiv.appendChild(linkButton);
                        });

                        sharedContentElement.appendChild(linkGroupDiv);
                    }
                }
            });
        }

        // Carrega os links compartilhados ao carregar a página
        updateSharedFeed();
    </script>
</body>
</html>
