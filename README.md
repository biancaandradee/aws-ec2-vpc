# Criando VPC e EC2 (AWS)

## CRIANDO VPC:
1. Primeiramente, cria-se uma VPC
- É necessária a definição de um IPv4 (CIDR RFC 1918 - https://docs.aws.amazon.com/pt_br/workspaces/latest/adminguide/a\mazon-workspaces-vpc.html);
2. Posteriormente, deve-se criar as subnets com os IPs calculados a partir do IP do VPC (https://www.site24x7.com/pt/tools/ipv4-sub-rede-calculadora.html);
3. Depois, cria-se um Internet Gateway, associando-o ao VPC criado;
4. Cria-se uma Route Table (RT) pública (conecta-se à Internet por meio do Internet Gateway) e uma Route Table privada (não tem conexão com o Internet Gateway);
5. É necessária a associação das subnets públicas à RT pública e as subnets privadas à RT privada;
6. Por fim, precisa associar a VPC a um ACL, no qual deve-se editar as Inbound/Outbound Rules, permitindo o tráfego.

## CRIANDO EC2:
1. Escolhe-se a AMI e a instância;
2. Configura-se a qual subnet a EC2 ficará atrelada;
- Se escolhida uma subnet pública, ela terá acesso à Internet; caso seja privada, não terá. Além disso, para ter acesso, gera-se um IPv4 automaticamente (enable auto-assign IPv4).
3. Adiciona-se Tags - para uma identificação mais fácil da instância; 
4. Configura-se o  Security Group - podendo criar um novo ou adicionar a um existente.
- Source: se for 0.0.0.0./0, pode ser acessado por qualquer IP da internet - porém, apenas pessoas autenticadas pelo type (por padrão, SSH).
- Type: se instalado o Nginx, é necessária a criação de uma nova regra do tipo HTTP. Por padrão, há também a regra SSH.
5. Clica-se em Launch - precisa da criação de uma chave SSH;
6. Faz-se o download da chave (.pem) e acontece o launch.

## CONECTANDO-SE À INSTÂNCIA PELA SSH - CHAVE PEM
1. Abre-se o terminal;
2. Localiza-se a pasta na qual está a chave;
3. Para que a chave não possa ser alterada e, sim, só possa ser lida, executamos chmod 400 nomeDoArquivoChave.extensao. No caso, temos chmod 400 ServidorWeb.pem
Conectar à instância usando a DNS pública: ssh -i “nomeDaChave.extensao” ubuntu@ec2 … ⇒ Sempre pegar no Conectar-se à instância > Cliente SSH!
No caso de ter se conectado por uma SSH criada no próprio computador, o arquivo a ser enviado é o .pub. Agora, estamos dentro do nosso Linux, podendo usar todos os comandos Linux normalmente.