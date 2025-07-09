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