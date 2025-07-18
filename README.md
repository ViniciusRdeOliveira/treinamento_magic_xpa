# Treinamento realizado na empresa Adderi em São Leopoldo/RS sobre a tecnologia Magic xpa
## Aprendizado e práticas com a plataforma de desenvolvimento low-code Magic XPA

<p>
  <strong>Magic xpa</strong> é uma plataforma de desenvolvimento <em>low-code</em> que permite criar aplicações empresariais multi-dispositivo de forma rápida e eficiente, com pouco código manual. Ela facilita a integração com diferentes sistemas, oferece ferramentas para desenvolvimento visual e agiliza a entrega de soluções corporativas.
</p>


## Anotações Gerais:
<ul>
<li>O curso está hospedado neste<a href="https://magic.echo.timetoknow.com/index.html#/$/library/channel/42e5487f-29b9-4e02-b1f8-dc8349bdae35/Iniciando%20com%20Magic%20xpa%20%26%20RIA%20Mobile?levelIds=YTkzZDI2YTAtYTg0MS00NDdhLWE0MDMtN2FjZDVmM2Y3NzNjLGU4YjYxZGU2LWNlNWUtNDRiNC05ZjNmLTQ3ZWZkMDYyZDk1ZiwxMDUzZmE1ZS04NmZiLTQxZDItOTJiOS05YTkzN2ZiYTczODY="> link</a> e seu acesso foi fornecido pela própria Adderi.</li>
<li>Os arquivos usados durante o treinamento estão hospedados neste <a href="https://drive.google.com/drive/folders/15lPJszq1rnQ1nZB25AMIwSTXcZ63-uRB?usp=sharing">link</a>
<li style="font-weight: bold; background-color: yellow;">Ao realizar a configuração do ambiente, ao configurar o arquivo DevProps.txt, ficar atento ao caminho da propriedade que define o IP (verificar ip da maquina pelo cmd usando ipconfig) e ajustar caso esteja diferente.</li>
<li style="font-weight: bold; background-color: yellow;">Ao realizar a configuração do ambiente, ao configurar arquivo DevProps.txt, verificar a propriedade que possui o PATH da pasta de scripts. Dependendo da versão do Magic XPA utilizada, o nome e o path da pasta pode ser diferente da especificada no arquivo DevProps.txt.</li>
<li>Ao realizar Configurações de ambiemte pelo menu Property Application, somente será valido para o projeto ATUAL.</li>
<li>Para Configurações Genéricas (valido para todos os projetos), a configuração deve ser feita pelo menu Optinons > Settings.</li>
<li>Heranças não são herdadas automaticamente se a propriedade já foi alterada manualmente antes</li>
<li>O Engine do Magic é orientado a Eventos. Metodologia orientada a evento funciona em 3 partes. Evento, uma trigger e um handler. Os eventos podem ser internos ou criados pelo usuário(Desenvolvido). Trigger pode ser interno, feito pelo desenvolvedor ou acionado pelo usuário. Handler são operações efetuadas quando um evento é disparado.</li>
<li><upper><b>>>>Strings iniciam com índice 1<<<</b></upper></li>
<br>
<h3>Breve Resumo Sobre Execução</h3>
<br>
<table>
  <thead>
    <tr>
      <th>Nome da unidade lógica</th>
      <th>Gatilho</th>
      <th>Quantidade de execuções</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Task Prefix</td>
      <td>Início da execução da tarefa</td>
      <td>1 vez</td>
    </tr>
    <tr>
      <td>Task Suffix</td>
      <td>Execução da tarefa é finalizada</td>
      <td>1 vez</td>
    </tr>
    <tr>
      <td>Record Prefix</td>
      <td>Obtenção do registro</td>
      <td>1 vez por registro</td>
    </tr>
    <tr>
      <td>Record Suffix</td>
      <td>A manipulação do registro é finalizada</td>
      <td>0 a 2 por registro</td>
    </tr>
    <tr>
      <td>Control Prefix</td>
      <td>O usuário final para em um controle</td>
      <td>-</td>
    </tr>
    <tr>
      <td>Control Verification</td>
      <td>O usuário deixa o controle, antes do Control Suffix</td>
      <td>-</td>
    </tr>
    <tr>
      <td>Control Suffix</td>
      <td>O usuário deixa o controle</td>
      <td>-</td>
    </tr>
    <tr>
      <td>Variable Change</td>
      <td>O valor da variável é alterado</td>
      <td>-</td>
    </tr>
  </tbody>
</table>
<br>
<h3>Regras de Execuão</h3>
<br>
<table>
  <thead>
    <tr>
      <th>Nome da unidade lógica</th>
      <th>Gatilho</th>
      <th>Próxima unidade lógica</th>
      <th>Próxima unidade lógica será executada se:</th>
      <th>Caso contrário, executará</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Task Prefix</td>
      <td>execução da tarefa</td>
      <td>Record Prefix</td>
      <td>existe pelo menos 1 registro no <em>data view</em></td>
      <td>Task Suffix</td>
    </tr>
    <tr>
      <td>Record Prefix</td>
      <td>o registro é obtido</td>
      <td>Control Prefix</td>
      <td>esta é uma tarefa <em>Online</em> ou <em>Rich Client</em></td>
      <td>Record Suffix</td>
    </tr>
    <tr>
      <td>Control Prefix</td>
      <td>o cursor para no controle</td>
      <td>Control Verification</td>
      <td>sem restrição</td>
      <td></td>
    </tr>
    <tr>
      <td>Control Verification</td>
      <td>a edição do controle é finalizada ou o cursor pula o controle</td>
      <td>Control Suffix</td>
      <td>sem restrição</td>
      <td></td>
    </tr>
    <tr>
      <td>Control Suffix</td>
      <td>a edição do controle é encerrada</td>
      <td>Variable Change</td>
      <td>o valor da variável mudou</td>
      <td>Record Suffix</td>
    </tr>
    <tr>
      <td>Variable Change</td>
      <td>o valor da variável é alterado</td>
      <td>Record Suffix</td>
      <td>o registro está prestes a ser salvo em uma tarefa <em>Online</em> ou <em>Rich Client</em></td>
      <td>Task Suffix</td>
    </tr>
    <tr>
      <td>Record Suffix</td>
      <td>o registro está prestes a ser salvo</td>
      <td>Task Suffix</td>
      <td>sem restrição</td>
      <td></td>
    </tr>
    <tr>
      <td>Task Suffix</td>
      <td>a tarefa está prestes a finalizar</td>
      <td>-</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>

<li>Toda vez que tiver mais de um evento de mesma propriedade o Magic XPA irá executar somente o ultimo da lista. Salvo excessão se alterar as propriedades do ultimo evento criado (com o mesmo nome) e alterar a opção <b>Propagate</b>no Handlers do Evento</li>
<li>Função <b>TRIM</b> remove espaços que podem conter antes e depois da string.</li>
<li><b>LoopCounter()</b> é uma função que retorna  o número de  interações.</li>
<li>A função <b>len</b> traz o tamanho de um caractere (lenght)</li>
<li>A função <b>CndRange</b> é utilizada para verificar se um valor está dentro de um intervalo definido de valores. É comumente usada em expressões condicionais, especialmente para simplificar verificações de múltiplos valores.</li>
<li>A função Mid no Magic xpa é usada para extrair uma substring (parte de uma string) a partir de uma posição específica, com um tamanho definido.<br><br>
Mid(string, start, length)<br><br>
Mid('123.456.789-00', 5, 3) -> Retorna: '456'<br><br>
Mid('Vinicius', 1, 3) -> Retorna: 'Vin'<br><br>
<li>A função <b>Stat</b> é usada para obter estatísticas sobre um arquivo, como se ele existe, seu tamanho, data de modificação etc.<br>
Stat( FileName, StatType )</li><br>

<b>FileName:</b> caminho completo (ou relativo) do arquivo.<br><br>
<b>StatType:</b> número que indica o tipo de informação desejada.<br><br>

<table>
  <thead>
    <tr>
      <th><strong>Nome Lógico</strong></th>
      <th><strong>Exemplo de Caminho / Valor Retornado</strong></th>
      <th><strong>Descrição / Função</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>%WorkingDir%</td>
      <td>C:\MeusApps\AppX</td>
      <td>Diretório onde a aplicação está sendo executada. Usado para localizar arquivos locais no contexto do usuário.</td>
    </tr>
    <tr>
      <td>%EngineDir%</td>
      <td>C:\Magicxpa\Runtime</td>
      <td>Diretório de onde a engine Magic está rodando. Útil para localizar DLLs e arquivos essenciais.</td>
    </tr>
    <tr>
      <td>%TempDir%</td>
      <td>C:\Users\Vinicius\AppData\Local\Temp</td>
      <td>Diretório temporário da aplicação em tempo de execução.</td>
    </tr>
    <tr>
      <td>%ProgramData%</td>
      <td>C:\ProgramData\Magic Software</td>
      <td>Armazena dados compartilhados da aplicação, especialmente em ambientes multiusuário.</td>
    </tr>
    <tr>
      <td>%LocalAppData%</td>
      <td>C:\Users\Vinicius\AppData\Local</td>
      <td>Diretório para cache e dados locais do usuário que não são sincronizados.</td>
    </tr>
    <tr>
      <td>%AppData%</td>
      <td>C:\Users\Vinicius\AppData\Roaming</td>
      <td>Diretório de dados do usuário com possibilidade de roaming (sincronização).</td>
    </tr>
    <tr>
      <td>%UserProfile%</td>
      <td>C:\Users\Vinicius</td>
      <td>Diretório base do perfil do usuário logado.</td>
    </tr>
    <tr>
      <td>%MagicEnvDir%</td>
      <td>(depende do ambiente)</td>
      <td>Diretório de definição do ambiente Magic (arquivo .edp).</td>
    </tr>
    <tr>
      <td>%MainProgDir%</td>
      <td>(depende do programa principal)</td>
      <td>Diretório onde está o programa principal da aplicação em execução.</td>
    </tr>
    <tr>
      <td>%ResourceDir%</td>
      <td>(configurado no projeto)</td>
      <td>Diretório de recursos (imagens, ícones, etc).</td>
    </tr>
    <tr>
      <td>%RIAModulesDir%</td>
      <td>(configurado para uso Rich Client)</td>
      <td>Diretório onde os módulos RIA são armazenados localmente.</td>
    </tr>
    <tr>
      <td>%GigaInitDir%</td>
      <td>C:\Magicxpa\Init</td>
      <td>Diretório de inicialização e configuração do Magic (ex: magic.ini).</td>
    </tr>
    <tr>
      <td>%ProgramFiles%</td>
      <td>C:\Program Files\Magic Software</td>
      <td>Diretório padrão de instalação em sistemas Windows.</td>
    </tr>
  </tbody>
</table>
<br>
<table>
  <thead>
    <tr>
      <th>Código</th>
      <th>Retorna</th>
      <th>Exemplo Magic xpa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>Arquivo existe (1 = sim, 0 = não)</td>
      <td>Stat('c:\\temp\\arquivo.txt', 1)</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Tamanho do arquivo (em bytes)</td>
      <td>Stat('c:\\temp\\arquivo.txt', 2)</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Data de criação</td>
      <td>Stat('c:\\temp\\arquivo.txt', 3)</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Hora de criação</td>
      <td>Stat('c:\\temp\\arquivo.txt', 4)</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Data da última modificação</td>
      <td>Stat('c:\\temp\\arquivo.txt', 5)</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Hora da última modificação</td>
      <td>Stat('c:\\temp\\arquivo.txt', 6)</td>
    </tr>
    <tr>
      <td>7</td>
      <td>Nome do drive</td>
      <td>Stat('c:\\temp\\arquivo.txt', 7)</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Atributos do arquivo</td>
      <td>Stat('c:\\temp\\arquivo.txt', 8)</td>
    </tr>
  </tbody>
</table>
<br>
<table>
  <thead>
    <tr>
      <th>Modo</th>
      <th>Descrição</th>
      <th>Comando Exemplo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>'C'</td>
      <td>Cria um novo arquivo (sobrescreve se existir)</td>
      <td>FileOpen('c:\\temp\\saida.txt', 'C')</td>
    </tr>
    <tr>
      <td>'A'</td>
      <td>Abre para adicionar ao final (append), cria se não existir</td>
      <td>FileOpen('c:\\temp\\log.txt', 'A')</td>
    </tr>
    <tr>
      <td>'R'</td>
      <td>Abre apenas para leitura</td>
      <td>FileOpen('c:\\temp\\entrada.txt', 'R')</td>
    </tr>
    <tr>
      <td>'U'</td>
      <td>Atualiza (leitura e gravação sem sobrescrever)</td>
      <td>FileOpen('c:\\temp\\dados.txt', 'U')</td>
    </tr>
    <tr>
      <td>'Q'</td>
      <td>Consulta: abre o arquivo apenas se existir</td>
      <td>FileOpen('c:\\temp\\check.txt', 'Q')</td>
    </tr>
  </tbody>
</table>
<br>
<h3>Relacionamento Um para Um x Um para Muitos</h3>

<p>
    No <strong>Magic xpa</strong> você pode estabelecer os dois seguintes relacionamentos entre fonte de dados:
</p>
<ul>
    <li>Um para um</li>
    <li>Um para muitos</li>
</ul>

<p>Abaixo, a comparação entre os relacionamentos:</p>

<table border="1" cellpadding="8" cellspacing="0">
    <thead>
        <tr>
            <th>Um para Um</th>
            <th>Um para Muitos</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Variáveis comuns são usadas para manter a conexão</td>
            <td>Variáveis comuns são usadas para manter a conexão</td>
        </tr>
        <tr>
            <td>A fonte principal e as fontes vinculadas (<em>linked</em>) são definidas na mesma tarefa</td>
            <td>Cada fonte de dados é definida como fonte principal em tarefas diferentes</td>
        </tr>
        <tr>
            <td>A fonte de dados vinculada retorna apenas um registro</td>
            <td>Cada registro pode retornar vários registros</td>
        </tr>
        <tr>
            <td>O mecanismo de recálculo do Magic xpa é responsável por manter a conexão</td>
            <td>
                O <em>range</em> da tarefa é responsável por manter a conexão, de acordo com parâmetro passado.<br>
                Além disso, o mecanismo de controle do Subform do Magic xpa também é responsável por manter a conexão.
            </td>
        </tr>
    </tbody>
</table>
<br>
<table>
  <thead>
    <tr>
      <th>Tipo de Link</th>
      <th>Descrição</th>
      <th>Uso Principal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Link Query</td>
      <td>Permite acesso somente leitura aos registros da subtarefa.</td>
      <td>Visualizar dados relacionados sem alterar.</td>
    </tr>
    <tr>
      <td>Link Write</td>
      <td>Permite leitura e escrita (edição, exclusão, inserção).</td>
      <td>Editar ou incluir dados em subtarefas.</td>
    </tr>
    <tr>
      <td>Link Inner Join</td>
      <td>Exibe apenas registros com correspondência entre as tarefas.</td>
      <td>Relacionamentos obrigatórios, como pedidos com clientes existentes.</td>
    </tr>
    <tr>
      <td>Link Outer Join</td>
      <td>Exibe todos os registros da tarefa principal, com ou sem correspondência na secundária.</td>
      <td>Relacionamentos opcionais, como clientes sem pedidos.</td>
    </tr>
    <tr>
      <td>Link Range</td>
      <td>Filtra registros com base em um intervalo (range) de valores.</td>
      <td>Exibir dados entre datas, faixas de ID, etc.</td>
    </tr>
    <tr>
      <td>Link Expression</td>
      <td>Usa uma expressão booleana para definir o vínculo entre registros.</td>
      <td>Filtragem dinâmica com múltiplas condições.</td>
    </tr>
    <tr>
      <td>Link Condition</td>
      <td>Define condições específicas baseadas em campos relacionados.</td>
      <td>Condicional entre campos, como Order.CustomerID = Customer.ID.</td>
    </tr>
    <tr>
      <td>Link Virtual</td>
      <td>Cria um link lógico sem acessar dados diretamente.</td>
      <td>Usado para controle de interface, lógica ou placeholders.</td>
    </tr>
  </tbody>
</table>
<br>
<h2>Operações Client-Side x Server-Side</h2>
<p>Algumas operações internas do Magic xpa são client-side e outras server-side.</p>

<table>
  <thead>
    <tr><th>Operação</th><th>Onde é executada</th></tr>
  </thead>
  <tbody>
    <tr><td>Verify</td><td>Client</td></tr>
    <tr>
      <td>Call</td>
      <td>
        <strong>Mixed</strong>: um Call para uma tarefa <em>Rich Client</em> usando a propriedade <em>Destination</em>. Há acesso imediato ao <strong>client</strong> para fechar a tarefa que está sendo executada no <em>Subform</em> naquele momento.<br>
        <strong>Server</strong>: outras chamadas são consideradas como <strong>Server</strong>, pois ocorre acesso ao <strong>server</strong> para iniciar a tarefa que está sendo chamada.
      </td>
    </tr>
    <tr>
      <td>Update</td>
      <td>Depende da variável que está sendo atualizada e da expressão usada para atualizá-la.</td>
    </tr>
    <tr>
      <td>Invoke</td>
      <td>
        <strong>Server</strong> – UDP, Web S, Web S Lite<br>
        <strong>Client e Server</strong> – OS Cmd<br>
        <strong>COM</strong> – Não suportado em tarefas <em>Rich Client</em>
      </td>
    </tr>
    <tr>
      <td>Raise Event</td>
      <td>É determinado pelo lado de execução do <em>handler</em> do evento.</td>
    </tr>
    <tr>
      <td>Evaluate</td>
      <td>Pode ser executado tanto no lado do <strong>client</strong> quanto no do <strong>server</strong> dependendo da operação.</td>
    </tr>
    <tr>
      <td>Block</td>
      <td>Pode ser executado tanto no lado do <strong>client</strong> quanto no <strong>server</strong> dependendo da operação.</td>
    </tr>
    <tr>
      <td>Form</td>
      <td>Não suportado em tarefas <em>Rich Client</em>. Você pode executar relatórios no <strong>server</strong> e exibí-los no <strong>client</strong>.</td>
    </tr>
    <tr>
      <td>Link Query</td>
      <td><strong>Server</strong>. É recomendado que você limite o uso de operações <em>Link</em>, pois elas são custosas em termos de interação com o <strong>server</strong>. Muitas vezes, você pode usar um controle <em>Data</em> ou <em>Inner Join</em>.</td>
    </tr>
  </tbody>
</table>
<br>
<h2>O Ciclo de Vida da Tarefa</h2>
<p>Quando estiver desenvolvendo programas <em>Rich Client</em>, algumas unidades lógicas são executadas no <strong>client</strong> e outras no <strong>server</strong>:</p>

<table>
  <thead>
    <tr><th>Operação</th><th>Onde é executada</th></tr>
  </thead>
  <tbody>
    <tr><td><em>Task Prefix</em></td><td><strong>Server</strong>. Nenhuma operação ou função <em>client-side</em> pode ser usada aqui.</td></tr>
    <tr><td><em>Task Suffix</em></td><td>Pode ser <strong>client</strong> ou <strong>server</strong>, dependendo das operações internas.</td></tr>
    <tr><td><em>Record</em></td><td>Pode ser <strong>client</strong> ou <strong>server</strong>. É recomendado que não se utilize funções e operações <strong>Server-side</strong> aqui para diminuir o acesso ao <strong>server</strong> quando estiver navegando pelos registros.</td></tr>
    <tr><td><em>Control</em></td><td>Pode ser <strong>client</strong> ou <strong>server</strong>. É recomendado que não se utilize funções e operações <strong>Server-side</strong> aqui para diminuir o acesso ao <strong>server</strong> ao percorrer os controles.</td></tr>
    <tr><td><em>Variable Change</em></td><td>Pode ser <strong>client</strong> ou <strong>server</strong>. É recomendado que não se utilize funções e operações <strong>Server-side</strong> aqui para diminuir o acesso ao <strong>server</strong> durante o mecanismo de recálculo ou quando alterar o valor do controle.</td></tr>
    <tr><td><em>Error</em></td><td><strong>Server</strong></td></tr>
  </tbody>
</table>
<br>
<h2>Identificando Atividades <em>Client</em> e <em>Server</em></h2>

<ul>
  <li>Como algumas operações são <em>client</em> e outras <em>server</em>, quando estiver desenvolvendo um programa é importante saber onde o programa pode ter problema de desempenho devido ao tráfego de/para do cliente e do servidor.</li>
  <li><strong>O Magic xpa</strong> fornece um auxílio visual exibindo o modo de cada <em>handler</em>, operação e função. Um caractere aparece à esquerda do número da linha e representa o modo, conforme abaixo:
    <ul>
      <li><strong>C</strong> – tratamento do lado do <em>client</em>.</li>
      <li><strong>S</strong> – tratamento do lado do <em>server</em>.</li>
      <li><strong>M</strong> – <em>Mixed</em>. A operação será executada em ambos, <em>client</em> e <em>server</em>.</li>
      <li><strong>U</strong> – <em>Unknown</em>. São para operações que o Studio não sabe onde será calculado.</li>
      <li><strong>E</strong> – <em>Error</em>. A operação não é suportada.</li>
    </ul>
  </li>
  <li>Se o caractere não aparecer, a entrada pode ser executada tanto no <em>client</em> quanto no <em>server</em>.</li>
</ul>
<br>
<h2>Cores da Operação <em>Rich Client</em></h2>
<p>A cor de fundo das operações no Editor de Tarefa indica se a operação é <strong>server-side</strong>, <strong>client-side</strong>, neutra ou desconhecida.</p>

<table>
  <thead>
    <tr><th>Nome da Cor</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>White (Branco)</td>
      <td>
        • Operações <strong>Client-side</strong> que precisam ser executadas no lado do <strong>client</strong><br>
        • Cabeçalhos de <em>handlers</em> que contêm operações no lado do <strong>client</strong><br>
        • Operações neutras que aparecem após uma operação <strong>client-side</strong><br>
        • Operações não suportadas, tais como operações mistas
      </td>
    </tr>
    <tr>
      <td style="background-color:#fbb4d4;">Server (Rosa)</td>
      <td>
        • Operações <strong>Server-side</strong> que precisam ser executadas no lado do <strong>server</strong><br>
        • Cabeçalhos de <em>handlers</em> que contêm operações no lado do <strong>server</strong><br>
        • Operações neutras que aparecem após uma operação <strong>server-side</strong>
      </td>
    </tr>
    <tr>
      <td style="background-color:#e0ffe0;">Unknown (Verde)</td>
      <td>
        • Operações de lado desconhecidas. Estas são operações nas quais o <em>Studio</em> não consegue identificar se serão executadas no lado do <strong>server</strong> ou <strong>client</strong>.
      </td>
    </tr>
  </tbody>
</table>

<p>Linhas neutras terão as mesmas cores da linha acima delas, pois elas serão executadas em qualquer lado que esteja fazendo o processamento.</p>
<br>
<table>
  <thead>
    <tr>
      <th colspan="2">Tarefas Rich Client x Batch</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rich Client</th>
      <th>Batch</th>
    </tr>
    <tr>
      <td>Permite interação com o usuário final</td>
      <td>Não permite interação com o usuário final</td>
    </tr>
    <tr>
      <td>O usuário final pode navegar entre os registros da fonte principal</td>
      <td>A tarefa verifica todos os registros da fonte principal dentro dos critérios do range. Se nenhuma fonte principal for definida ou a tarefa estiver no modo de criação, a tarefa será repetida até que a condição do End Task seja atendida.</td>
    </tr>
    <tr>
      <td>A unidade lógica do controle está disponível.</td>
      <td>A unidade lógica do controle não está disponível, uma vez que não há interação com o usuário final e o motor não para em nenhum controle.</td>
    </tr>
    <tr>
      <td>O motor lida com a lógica relacionada à navegação do usuário final.</td>
      <td></td>
    </tr>
    <tr>
      <td>A unidade lógica do Group não está disponível.</td>
      <td>A unidade lógica do Group está disponível e permite controlar grupos de dados.</td>
    </tr>
    <tr>
      <td>O formulário da tarefa é uma parte essencial da criação da tarefa e sua execução.</td>
      <td>O formulário da tarefa é opcional e na maioria das vezes ela não é usada.</td>
    </tr>
    <tr>
      <td>Se o dado for alterado, o Record Suffix é executado e o registro gravado.</td>
      <td>O Record Suffix é sempre executado.</td>
    </tr>
    <tr>
      <td>Os eventos são tratados quando a tarefa estiver ociosa.</td>
      <td>Os eventos são tratados a cada período de tempo ou a cada quantidade processada de registros.</td>
    </tr>
  </tbody>
</table>
<br>
<li>Todo programa Magic XPA tem como requerido ao menos uma variável criada (por mais que não seja usada, ela deve estar criada no Data View)</li>
<li><b>Falando sobre menus:</b> Quando pensado em usar no sistema windows, o menu deve ser vinculado a opção pulldown menu. Quando pensado em utilizar pelo mobile, deve-se utilizar a opção Navigation Drawer. A opção de Navigation Drawer irá exibir em tela o menu sanduiche.</li>
<li>Opções de Context Menu continuam iguais tanto Mobile quanto Desktop.</li>
<li>A opção <b>Action Bar Menu</b> irá fixar menus no mobile ao lado do menu sanduiche.</li>
<li>Para um programa online chamar um programa offline, deve-se utilizar um evento no Main Programam que faça o download dos dados do servidor para a execução offline.</li>
<li>Contato:<br>
(11) 30480700<br>
contato@magicsoftware.com.br</li>