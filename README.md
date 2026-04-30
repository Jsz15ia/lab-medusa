#  lab-medusa

Este projeto tem como objetivo simular ataques de força bruta em um ambiente controlado utilizando Kali Linux e Metasploitable 2, com foco na identificação de vulnerabilidades e aplicação de medidas de mitigação.

---

##  Ambiente de Testes

O laboratório foi configurado utilizando duas máquinas virtuais no VirtualBox:

- Kali Linux (máquina atacante)  
- Metasploitable 2 (máquina alvo vulnerável)  

Ambas foram conectadas em uma rede do tipo **Host-only**, permitindo comunicação direta entre elas sem acesso externo.

---

##  Metodologia

Inicialmente, foram criadas wordlists simples contendo possíveis nomes de usuários e senhas comuns. Essas listas foram utilizadas como base para simular ataques de força bruta, demonstrando como credenciais fracas podem ser facilmente exploradas.

Em seguida, foi desenvolvido um script em Bash para organizar e automatizar os testes realizados. Nesse script, foi definida uma variável chamada `IP`, responsável por armazenar o endereço da máquina alvo, permitindo reutilizar o mesmo valor em diferentes comandos.

O script inicia com a criação das wordlists utilizando o comando `echo`, que escreve diretamente os conteúdos nos arquivos de texto.

---

##  Ataques Realizados

###  FTP (Força Bruta)

Foi realizado um ataque de força bruta ao serviço FTP utilizando a ferramenta Medusa, com base nas wordlists criadas.

Após a execução do ataque, foi feito um teste de conexão via FTP para validar se alguma credencial foi comprometida com sucesso.

---

###  HTTP (DVWA)

Na sequência, foi executado um ataque a um formulário web da aplicação DVWA (Damn Vulnerable Web Application).

O Medusa foi configurado para simular requisições HTTP, enviando combinações de usuário e senha ao formulário de login. A ferramenta identifica tentativas bem-sucedidas com base na ausência da mensagem de erro definida no parâmetro de falha.

---

###  SMB (Enumeração e Password Spraying)

O script realizou a enumeração do serviço SMB utilizando a ferramenta `enum4linux`, coletando informações sobre usuários, compartilhamentos e configurações do sistema.

Os resultados foram salvos em um arquivo para análise posterior.

Com base nessas informações, foi executado um ataque de **password spraying**, testando uma mesma lista de senhas em múltiplos usuários, reduzindo o risco de bloqueio de contas.

Por fim, foi utilizado o comando `smbclient` para listar os compartilhamentos disponíveis no servidor, validando o acesso com credenciais obtidas.

---

##  Resultados

Durante os testes, foi possível observar que o uso de credenciais simples e previsíveis permitiu o acesso não autorizado a serviços como FTP e SMB.

A enumeração de serviços também revelou informações sensíveis que poderiam ser exploradas em cenários reais.

---

##  Medidas de Mitigação

- Utilização de senhas fortes e complexas  
- Implementação de políticas de bloqueio após múltiplas tentativas  
- Uso de autenticação multifator (MFA)  
- Restrição de acesso a serviços sensíveis  
- Monitoramento de tentativas de login  
- Substituição de protocolos inseguros (como FTP) por alternativas seguras (como SFTP)  
