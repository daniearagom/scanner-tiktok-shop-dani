# Scanner TikTok Shop Dani — MVP 0.2

Aplicação privada, mobile-first, com cadastro inicial de uma única conta por e-mail e senha.

## O que funciona nesta versão
- Criação da primeira conta (e-mail + senha de no mínimo 12 caracteres).
- Senha armazenada com hash bcrypt.
- Sessão em cookie HttpOnly, SameSite=Lax, com validade de 7 dias.
- Login e logout.
- Rotas de análise e upload exigem sessão.
- Upload e pré-visualização local de vídeo.
- Triagem heurística inicial de headlines/frases.

## Limitações
A análise automática de vídeo, extração de frames, transcrição de áudio e IA multimodal ainda não estão conectadas. O scanner de texto é uma triagem simples, não uma decisão oficial do TikTok e não garante aprovação.

## Instalação local
Requer Python 3.10+.

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
```

Crie `.env` a partir de `.env.example` e configure `SESSION_SECRET` com uma chave aleatória longa e exclusiva. Exemplo para gerar:
```bash
python -c "import secrets; print(secrets.token_urlsafe(48))"
```

Inicie:
```bash
uvicorn app.main:app --reload
```
Abra http://127.0.0.1:8000 e crie sua conta na primeira tela.

## Antes de publicar na internet
- Configure `COOKIE_SECURE=true` com HTTPS.
- Use HTTPS e um domínio privado.
- Configure backups protegidos e política de retenção/exclusão de vídeos.
- Adicione rate limiting, proteção CSRF apropriada e monitoramento de tentativas de login.
- Nunca compartilhe o `.env`, o banco `scanner_dani.sqlite3` ou a pasta `uploads`.
- O cadastro inicial é de uso único; não existe cadastro público de novos usuários.
