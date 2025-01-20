let amigos = [];

function adicionarAmigo() {
    const nomeInput = document.getElementById('amigo');
    const nome = nomeInput.value.trim();

    if (nome) {
        amigos.push(nome);
        nomeInput.value = '';  // Limpar o campo de input
        atualizarListaAmigos();
    }
}

function atualizarListaAmigos() {
    const lista = document.getElementById('listaAmigos');
    lista.innerHTML = ''; // Limpar a lista antes de atualizar

    amigos.forEach(amigo => {
        const li = document.createElement('li');
        li.textContent = amigo;
        lista.appendChild(li);
    });
}

function sortearAmigo() {
    if (amigos.length < 2) {
        alert('Adicione pelo menos dois amigos para realizar o sorteio!');
        return;
    }

    let sorteio = [];
    let copiaAmigos = [...amigos];

    // Sorteio sem repetição
    copiaAmigos.forEach(amigo => {
        let index = Math.floor(Math.random() * copiaAmigos.length);
        while (copiaAmigos[index] === amigo) {
            index = Math.floor(Math.random() * copiaAmigos.length); // Garantir que ninguém se tire
        }
        sorteio.push({ amigo, sorteado: copiaAmigos.splice(index, 1)[0] });
    });

    mostrarResultado(sorteio);
}

function mostrarResultado(sorteio) {
    const resultadoLista = document.getElementById('resultado');
    resultadoLista.innerHTML = ''; // Limpar o resultado

    sorteio.forEach(({ amigo, sorteado }) => {
        const li = document.createElement('li');
        li.textContent = `${amigo} tirou ${sorteado}`;
        resultadoLista.appendChild(li);
    });
}
