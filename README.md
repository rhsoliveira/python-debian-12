# Guia de Instalação: Python, Selenium, WebDriver, Chromium e Chrome no Debian/Ubuntu

Este guia fornece instruções para instalar todos os componentes necessários para automação web com Python e Selenium no Debian 12 e Ubuntu.

## 1. Atualizar o Sistema

```bash
sudo apt update
```

```bash
sudo apt upgrade -y
```

## 2. Instalar Python e pip

```bash
sudo apt install -y python3 python3-pip
```

## 3. Instalar Chromium e ChromeDriver

```bash
sudo apt install -y chromium chromium-driver
```

Para verificar a instalação:

```bash
chromium --version
chromedriver --version
```

## 4. Instalar Google Chrome (opcional)

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

```bash
sudo apt install -y ./google-chrome-stable_current_amd64.deb
```

## 5. Instalar Selenium

### Problema comum: "externally-managed-environment"

Nas versões recentes do Debian e Ubuntu, você pode encontrar este erro ao usar pip:

```
error: externally-managed-environment
× This environment is externally managed
```

### Opção 1: Instalar via apt (recomendado para ambiente de sistema)

```bash
sudo apt install python3-selenium
```

### Opção 2: Criar um ambiente virtual (melhor prática para desenvolvimento)

```bash
sudo apt install python3-full python3-venv
```

```bash
python3 -m venv ~/selenium_env
```

```bash
source ~/selenium_env/bin/activate
```

```bash
pip install selenium
```

### Opção 3: Usar pipx (bom para ferramentas isoladas)

```bash
sudo apt install pipx
```

```bash
pipx ensurepath
```

```bash
pipx install selenium
```

### Opção 4: Forçar a instalação (NÃO RECOMENDADO)

```bash
pip install selenium --break-system-packages
```

## 6. Instalação manual do WebDriver (opções alternativas)

### Usar WebDriver Manager (em ambiente virtual)

```bash
source ~/selenium_env/bin/activate
```

```bash
pip install webdriver-manager
```

Uso no código Python:

```python
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service

service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)
```

### Baixar ChromeDriver manualmente

```bash
wget https://chromedriver.storage.googleapis.com/$(curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE)/chromedriver_linux64.zip
```

```bash
unzip chromedriver_linux64.zip
```

```bash
sudo mv chromedriver /usr/local/bin/
```

```bash
sudo chmod +x /usr/local/bin/chromedriver
```

### Verificar caminho ChromeDriver

```bash
which chromedriver
```

## 7. Instalar Selenium

### Problema comum: "externally-managed-environment"

Nas versões recentes do Debian e Ubuntu, você pode encontrar este erro ao usar pip:

```
error: externally-managed-environment
× This environment is externally managed
```

### Opção 1: Instalar via apt (recomendado para ambiente de sistema)

```bash
sudo apt install python3-bs4
```

### Opção 2: Criar um ambiente virtual (melhor prática para desenvolvimento)

```bash
sudo apt install python3-full python3-venv
```

```bash
python3 -m venv ~/selenium_env
```

```bash
source ~/selenium_env/bin/activate
```

```bash
pip install beautifulsoup4 selenium webdriver-manager
```

### Opção 3: Usar pipx (bom para ferramentas isoladas)

```bash
sudo apt install pipx
```

```bash
pipx ensurepath
```

```bash
pipx install beautifulsoup4
```

### Opção 4: Forçar a instalação (NÃO RECOMENDADO)

```bash
pip install beautifulsoup4 --break-system-packages
```

## 8. Exemplo de código básico

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By

# Configurar o Chrome
chrome_options = Options()
chrome_options.add_argument("--headless")  # Opcional: executar sem interface gráfica
service = Service('/usr/bin/chromedriver')  # Caminho pode variar

# Iniciar o navegador
driver = webdriver.Chrome(service=service, options=chrome_options)

# Navegar para uma página
driver.get("https://www.google.com")

# Interagir com elementos
search_box = driver.find_element(By.NAME, "q")
search_box.send_keys("Selenium Python")
search_box.submit()

# Capturar resultados
results = driver.find_elements(By.CSS_SELECTOR, "h3")
for result in results[:5]:
    print(result.text)

# Fechar o navegador
driver.quit()
```

## Verificação da instalação

```bash
python3 --version
```

```bash
pip3 show selenium
```

```bash
chromedriver --version
```

```bash
chromium --version
```

# Guia de Instalação: PHP e Extensão cURL

Este guia explica como instalar o PHP e a extensão cURL no Debian/Ubuntu para execução de scripts que necessitam realizar requisições HTTP.

## Pré-requisitos

- Acesso root ou permissões sudo
- Terminal de linha de comando
- Sistema operacional Debian/Ubuntu

## Atualizar o Sistema

Antes de instalar qualquer pacote, é recomendável atualizar a lista de pacotes:

```bash
sudo apt update
```

```bash
sudo apt upgrade -y
```

## Instalação do PHP

Instale o PHP e os pacotes comuns:

```bash
sudo apt install -y php php-cli php-common
```

## Instalação da Extensão cURL para PHP

A extensão cURL permite que scripts PHP realizem requisições HTTP/HTTPS:

```bash
sudo apt install -y php-curl
```

## Instalação de Extensões PHP Adicionais (Opcional)

Dependendo das necessidades do seu projeto, você pode instalar outras extensões comuns:

```bash
sudo apt install -y php-json php-mbstring php-xml php-zip
```

## Verificar a Instalação

### Verificar a versão do PHP:

```bash
php -v
```

### Verificar se a extensão cURL está instalada:

```bash
php -m | grep curl
```

Ou de forma mais detalhada:

```bash
php -i | grep curl
```

## Executando Scripts PHP com cURL

Um exemplo básico de script PHP que utiliza cURL:

```php
<?php
// Inicializa uma sessão cURL
$ch = curl_init('https://api.exemplo.com/dados');

// Configura opções da requisição
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, true);

// Executa a requisição
$response = curl_exec($ch);

// Verifica erros
if (curl_errno($ch)) {
    echo 'Erro cURL: ' . curl_error($ch);
} else {
    echo 'Resposta: ' . $response;
}

// Fecha a sessão cURL
curl_close($ch);
?>
```

Para executar um script PHP pelo terminal:

```bash
php seu_script.php
```

## Solução de Problemas

### Se você receber o erro "Call to undefined function curl_init()":

Este erro indica que a extensão cURL não está instalada ou não está ativada:

1. Verifique se a extensão está instalada:
   ```bash
   apt list --installed | grep php-curl
   ```

2. Se não estiver instalada, instale-a:
   ```bash
   sudo apt install php-curl
   ```

3. Se estiver instalada, verifique se está ativada:
   ```bash
   php -i | grep curl
   ```

4. Pode ser necessário reiniciar serviços web após a instalação:
   ```bash
   sudo systemctl restart apache2
   ```
   ou
   ```bash
   sudo systemctl restart php-fpm
   ```

## Observações

- A versão do PHP e suas extensões podem variar dependendo da versão do sistema operacional
- Para ambientes de produção, considere configurações adicionais de segurança
- Mantenha o PHP e suas extensões atualizadas para evitar vulnerabilidades
