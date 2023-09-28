<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Divulgador de Rede Social</title>
    <!-- Inclua o link para a fonte Pacifico -->
    <link href="https://fonts.googleapis.com/css?family=Pacifico&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.3.1/firebase-database.js"></script>
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

        /* Estilos para o mural com os 1º, 2º e 3º lugares */
        #top-links {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }

        .top-link {
            flex: 1;
            background-color: #f7f7f7;
            padding: 10px;
            border-radius: 5px;
            text-align: center;
        }

        .top-link h2 {
            margin: 0;
        }

        .gold {
            background-color: gold; /* 1º lugar - cor dourada */
        }

        .silver {
            background-color: silver; /* 2º lugar - cor prata */
        }

        .bronze {
            background-color: #cd7f32; /* 3º lugar - cor bronze */
        }

        .top-link-url {
            text-decoration: none;
            color: #333;
        }
    </style>
</head>
<body>
    <main>
        <section id="points-wallet">
            <h2>Carteira de Pontos</h2>
            <p id="user-points">Pontos: 10</p>
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
            <section id="top-links">
                <div class="top-link gold">
                    <h2>1º Lugar</h2>
                    <a href="#" class="top-link-url">Link 1</a>
                </div>
                <div class="top-link silver">
                    <h2>2º Lugar</h2>
                    <a href="#" class="top-link-url">Link 2</a>
                </div>
                <div class="top-link bronze">
                    <h2>3º Lugar</h2>
                    <a href="#" class="top-link-url">Link 3</a>
                </div>
            </section>
            
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

    <!-- Adicione este código JavaScript abaixo da seção <script> existente em seu código -->
    <script>
        // ...
    
        // Função para compartilhar um link
        function compartilharLink(event) {
            event.preventDefault(); // Evita o comportamento padrão de envio do formulário
            const linkPostagem = document.getElementById("linkPostagem").value;
    
            if (linkPostagem) {
                const userId = firebase.auth().currentUser.uid; // Supondo que você tenha configurado a autenticação de usuário
    
                // Adicionar o link compartilhado ao banco de dados
                const novoLinkRef = database.ref("links").push();
                novoLinkRef.set({
                    userId: userId,
                    link: linkPostagem,
                    timestamp: firebase.database.ServerValue.TIMESTAMP,
                    curtidas: 0, // Inicialmente, o link não tem curtidas
                });
    
                document.getElementById("linkPostagem").value = "";
    
                // Verifica se atingiu 100 links compartilhados
                database.ref("links").once("value").then((snapshot) => {
                    const numLinks = snapshot.numChildren();
    
                    if (numLinks >= 100) {
                        // Quando atingir 100 links, classifique e mova os mais curtidos
                        classificarEMoverLinksMaisCurtidos();
                    }
                });
            }
        }
    
        // Função para classificar e mover os links mais curtidos para as posições
        function classificarEMoverLinksMaisCurtidos() {
            const linksRef = database.ref("links");
    
            linksRef
                .orderByChild("curtidas") // Classifique pelos links mais curtidos
                .limitToLast(3) // Pegue os 3 links mais curtidos
                .once("value")
                .then((snapshot) => {
                    // Obtém os links mais curtidos
                    const linksMaisCurtidos = [];
    
                    snapshot.forEach((linkSnapshot) => {
                        linksMaisCurtidos.push({
                            key: linkSnapshot.key,
                            linkData: linkSnapshot.val(),
                        });
                    });
    
                    // Remove os links mais curtidos da lista original
                    linksMaisCurtidos.forEach((link) => {
                        linksRef.child(link.key).remove();
                    });
    
                    // Adiciona os links mais curtidos à seção de posições
                    adicionarLinksMaisCurtidosAoTopo(linksMaisCurtidos);
                });
        }
    
        // Função para adicionar os links mais curtidos à seção de posições
        function adicionarLinksMaisCurtidosAoTopo(linksMaisCurtidos) {
            const topLinks = database.ref("topLinks");
    
            linksMaisCurtidos.forEach((link) => {
                // Adicione os links mais curtidos à seção de posições (1º, 2º, 3º lugar)
                topLinks.push(link.linkData);
            });
        }
    
        // Evitar que o formulário recarregue a página ao ser enviado
        document.getElementById("postForm").addEventListener("submit", function (event) {
            event.preventDefault(); // Evita a submissão padrão do formulário
            compartilharLink(event);
        });
    
        // ...
    
    </script>
</body>
