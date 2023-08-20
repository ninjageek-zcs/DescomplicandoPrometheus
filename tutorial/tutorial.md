COMO INSTALAR O PROMETHEUS

 1 - Acessar o site de downloas do prometheus e copiar link do mesmo:
        
     https://prometheus.io/download/
     Copiar o link para o endereço da versão do prometheus desejada (de preferência a última versão);
 
 2 - Obter o prometheus referido via curl:

     curl -LO https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux amd64.tar.gz
      
 3 - Descompactar o tar obtido:
                
     tar -xvzf prometheus-2.46.0.linux-amd64.tar.gz
     
 4 - Mover os binários necessários
        
     Mover os binários do prometheus e promtool para /usr/local/bin com:
     mv prometheus-2.46.0.linux-amd64/prometheus /usr/local/bin 
     mv prometheus-2.46.0.linux-amd64/promtool /usr/local/bin
     
 5 - Criar diretório de configuração para o prometheus e mover os arquivos de configuração necessários   
 
     mkdir /etc/prometheus
     mv prometheus-2.46.0.linux-amd64/consoles /etc/prometheus/
     mv prometheus-2.46.0.linux-amd64/console_libraries/ /etc/prometheus/ 
     Mover o prometheus-2.46.0.linux-amd64/prometheus.yml para /etc/prometheus 
     ou copiar o arquivo prometheus.yml do diretório de configuração do repositório.

  6 - Criar diretório de dados do prometheus

     mkdir /var/lib/prometheus
       
  7 - Adicionar grupo e usuário para o prometheus 
      
     addgroup --system prometheus
     adduser --shell /sbin/nologin --system --group prometheus
           
     Verificar se grupo e usuário prometheus foram criados com:

     cat /etc/group | grep prometheus
     cat /etc/passwd | grep prometheus

  8 - Dar as permissões para o usuário do prometheus aos seguintes diretórios:

     chown prometheus:prometheus /etc/prometheus
     chown prometheus:prometheus /var/lib/prometheus
        
  9 - Criar serviço no systemd para o prometheus
          
     Copiar o arquivo prometheus.service do diretório de configuração do repositório para 
     /etc/systemd/system/prometheus.service.
     Depois executar:                                          
     systemctl daemon-reload

 10 - Iniciar o prometheus e habilitá-lo na inicialização:
           
     systemctl start prometheus
     systemctl enable prometheus

 11 - Validar funcionamento
           
     systemctl status prometheus
     curl localhost:9090 ou acessar http://localhost:9090
             
             
