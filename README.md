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
    </style>
</head>
<body>
    
    <header>
        <h1>Divulgador De Rede Social</h1>
        <button id="loginButton">Entrar com o Google</button>
    </header>
    
    <main>
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
        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        // Referências ao banco de dados e autenticação
        const database = firebase.database();
        const auth = firebase.auth();

        // Variável para armazenar a quantidade de pontos do usuário
        let userPoints = 20; // Defina a carteira com 20 pontos iniciais

        // Atualize a exibição da carteira de pontos
        function updatePointsDisplay() {
            const userPointsElement = document.getElementById('user-points');
            userPointsElement.textContent = 'Pontos: ' + userPoints;
        }

        // Deduza 2 pontos da carteira quando um link for compartilhado
        function deductPoints() {
            userPoints -= 2; // Deduz 2 pontos da carteira
            updatePointsDisplay(); // Atualiza a exibição da carteira de pontos
        }

        // Função para verificar se um link já foi compartilhado
        function isLinkShared(link) {
            const sharedLinksRef = database.ref('sharedLinks');
            return sharedLinksRef.once('value').then(function(snapshot) {
                const links = snapshot.val();
                if (links) {
                    return Object.values(links).includes(link);
                }
                return false;
            });
        }

        // Função para adicionar conteúdo compartilhado
        function addSharedContent(content) {
            // Verifica se o link já foi compartilhado
            return isLinkShared(content).then(function(alreadyShared) {
                if (!alreadyShared) {
                    // Gere uma chave única para cada link compartilhado
                    const newContentKey = database.ref('sharedLinks').push().key;
                    const updates = {};
                    updates['/sharedLinks/' + newContentKey] = content;
                    database.ref().update(updates);
                    deductPoints(); // Deduz 2 pontos da carteira
                } else {
                    alert('Este link já foi compartilhado anteriormente.');
                }
            });
        }

        // Função para atualizar a exibição dos links compartilhados
        function updateSharedFeed() {
            const sharedContent = document.getElementById('sharedContent');
            sharedContent.innerHTML = ''; // Limpa o conteúdo atual

            // Consulta os links compartilhados no banco de dados
            const sharedLinksRef = database.ref('sharedLinks');
            sharedLinksRef.on('child_added', function (data) {
                const linkKey = data.key;
                const link = data.val();
                const feedItem = document.createElement('div');
                feedItem.className = 'postagem';

                // Botão "Acesso ao Link"
                const openLinkButton = document.createElement('button');
                openLinkButton.textContent = 'Acesso ao Link';
                openLinkButton.addEventListener('click', function () {
                    window.open(link, '_blank'); // Abre o link em uma nova guia
                });

                // Botão "Curtir"
                const likeButton = document.createElement('button');
                likeButton.textContent = 'Curtir';
                likeButton.addEventListener('click', function () {
                    likeSharedLink(linkKey);
                });

                feedItem.appendChild(openLinkButton);
                feedItem.appendChild(likeButton);
                feedItem.style.marginBottom = '10px'; // Adicione uma margem inferior de 10px entre os botões

                sharedContent.appendChild(feedItem);
            });
        }

        // Função para processar o formulário de compartilhamento de perfil
        const postForm = document.getElementById('postForm');
        postForm.addEventListener('submit', function (e) {
            e.preventDefault(); // Impede o envio padrão do formulário

            const linkPostagem = document.getElementById('linkPostagem').value;
            if (linkPostagem && userPoints >= 2) { // Verifica se o usuário tem pelo menos 2 pontos para compartilhar
                addSharedContent(linkPostagem).then(function () {
                    document.getElementById('linkPostagem').value = ''; // Limpa o campo após o compartilhamento
                });
            } else {
                alert('Você não tem pontos suficientes para compartilhar ou o link já foi compartilhado.');
            }
        });

        // Atualize o estado do botão de compartilhamento com base nos pontos disponíveis
        function updateShareButtonState() {
            const linkPostagem = document.getElementById('linkPostagem');
            const shareButton = document.querySelector('#postForm button[type="submit"]');
            
            if (userPoints < 2 || !linkPostagem.value) {
                shareButton.disabled = true;
            } else {
                shareButton.disabled = false;
            }
        }

        // Inicialize a atualização dos links compartilhados
        updateSharedFeed();

        // Atualize a exibição dos pontos e o estado do botão de compartilhamento
        updatePointsDisplay();
        updateShareButtonState();

        // Adicione um ouvinte de evento para o botão de login
        const loginButton = document.getElementById('loginButton');
        loginButton.addEventListener('click', function() {
            // Autenticação com o Google
            const provider = new firebase.auth.GoogleAuthProvider();
            auth.signInWithPopup(provider).then(function(result) {
                // O usuário fez login com sucesso, você pode adicionar lógica adicional aqui
                const user = result.user;
                console.log('Login bem-sucedido:', user);
            }).catch(function(error) {
                // Tratar erros de login aqui
                console.error('Erro de login:', error);
            });
        });
    </script>
</body>
