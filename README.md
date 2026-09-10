# Teste
Script teste
import os
import logging
from flask import Flask, request

app = Flask(__name__)

# Configuração de logging seguro
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s',
    filename='app_secure.log'
)

@app.route('/login', methods=['POST'])
def login():
    # Em uma aplicação real, use banco de dados e hashes de senha
    email = request.form.get('email')
    # NUNCA registre a senha real no log
    password = request.form.get('password') 
    
    if not email or not password:
        return "Entrada inválida", 400

    # Registra a tentativa sem expor dados sensíveis
    logging.info(f"Tentativa de login para o usuário: {email} a partir do IP: {request.remote_addr}")

    # Prosseguir com a lógica de autenticação...
    return "Processo de login iniciado."

if __name__ == '__main__':
    # Use um servidor WSGI de produção como Gunicorn em ambientes reais
    app.run(debug=False, port=5000)
