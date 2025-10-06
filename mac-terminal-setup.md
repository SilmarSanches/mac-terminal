# 🚀 Guia Completo: Setup do Terminal no Mac

Configuração completa de um terminal moderno no macOS com Oh My Zsh, Powerlevel10k, tmux e ferramentas visuais.

## 📋 Índice

- [Pré-requisitos](#pré-requisitos)
- [Instalação Passo a Passo](#instalação-passo-a-passo)
- [Atalhos do tmux](#atalhos-do-tmux)
- [Comandos Úteis](#comandos-úteis)
- [Troubleshooting](#troubleshooting)

---

## Pré-requisitos

- macOS (qualquer versão recente)
- Terminal padrão do Mac ou iTerm2
- Conexão com internet

---

## Instalação Passo a Passo

### 1. Instalar o Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

### 2. Instalar Nerd Font (para ícones)

```bash
brew install font-meslo-lg-nerd-font
```

**Configurar a fonte no Terminal:**

1. Terminal → **Preferências** (`Cmd + ,`)
2. Aba **Perfis** → Aba **Texto**
3. **Fonte** → **Alterar** → Selecione **MesloLGS NF**
4. Tamanho: **12-14pt**

**Configurar tecla Option (para navegação com Alt):**

1. Ainda em **Preferências** → Aba **Teclado**
2. Marque: **"Usar a tecla Option como tecla Meta"**

---

### 3. Instalar Oh My Zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

---

### 4. Instalar Powerlevel10k (tema)

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

---

### 5. Instalar plugins do Zsh

```bash
# zsh-autosuggestions (sugestões enquanto digita)
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting (destaca comandos válidos)
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

---

### 6. Instalar tmux

```bash
brew install tmux
```

**Criar arquivo de configuração do tmux:**

```bash
nano ~/.tmux.conf
```

**Cole esta configuração completa:**

```bash
# Prefixo mais fácil: Ctrl+a (em vez de Ctrl+b)
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# Dividir painéis com atalhos fáceis
bind | split-window -h    # Ctrl+a depois |  (vertical)
bind - split-window -v    # Ctrl+a depois -  (horizontal)
unbind '"'
unbind %

# Navegar entre painéis com Ctrl+a + setas
bind Left select-pane -L
bind Right select-pane -R
bind Up select-pane -U
bind Down select-pane -D

# Navegação estilo Vim (h j k l)
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# Redimensionar painéis
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5

# Recarregar config facilmente
bind r source-file ~/.tmux.conf \; display "✓ Config recarregada!"

# Melhorias visuais e usabilidade
set -g mouse on                    # Habilitar mouse
set -g base-index 1               # Janelas começam em 1
setw -g pane-base-index 1         # Painéis começam em 1
set -g status-style bg=colour235,fg=colour136
```

**Salvar:** `Ctrl+O` → `Enter` → `Ctrl+X`

---

### 7. Instalar eza (ls com ícones)

```bash
brew install eza
```

---

### 8. Configurar o .zshrc

```bash
nano ~/.zshrc
```

**Procure e modifique estas seções:**

```bash
# Tema do Oh My Zsh
ZSH_THEME="powerlevel10k/powerlevel10k"

# Plugins (procure a linha que começa com plugins=)
plugins=(
  git
  tmux
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

**Adicione no FINAL do arquivo:**

```bash
# Aliases do eza para ls com ícones
alias ls='eza --icons'
alias ll='eza --icons -l'
alias la='eza --icons -la'
alias lt='eza --icons --tree --level=2'
alias l='eza --icons -lah'

# Melhorar autocomplete
autoload -Uz compinit && compinit
zstyle ':completion:*' menu select
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
```

**Salvar:** `Ctrl+O` → `Enter` → `Ctrl+X`

---

### 9. (Opcional) Desabilitar módulo Google Cloud

Se não quiser ver informações do Google Cloud no prompt:

```bash
mkdir -p ~/.config
nano ~/.config/starship.toml
```

**Cole:**

```toml
[gcloud]
disabled = true
```

**Salvar:** `Ctrl+O` → `Enter` → `Ctrl+X`

---

### 10. Aplicar configurações

```bash
source ~/.zshrc
```

---

### 11. Configurar Powerlevel10k

```bash
p10k configure
```

Siga o assistente interativo escolhendo suas preferências visuais.

**Dica:** Se aparecerem interrogações (?) em vez de ícones, volte e verifique se a fonte MesloLGS NF está configurada corretamente no Terminal.

---

## ⌨️ Atalhos do tmux

### Gerenciamento de Painéis

| Atalho | Ação |
|--------|------|
| `Ctrl+a` depois `\|` | Dividir verticalmente |
| `Ctrl+a` depois `-` | Dividir horizontalmente |
| `Ctrl+a` depois `←→↑↓` | Navegar entre painéis (setas) |
| `Ctrl+a` depois `h j k l` | Navegar entre painéis (vim) |
| `Ctrl+a` depois `H J K L` | Redimensionar painéis |
| `Ctrl+a` depois `x` | Fechar painel atual |

### Gerenciamento de Sessões

| Atalho | Ação |
|--------|------|
| `Ctrl+a` depois `d` | Desconectar (sessão continua rodando) |
| `Ctrl+a` depois `c` | Criar nova janela |
| `Ctrl+a` depois `n` | Próxima janela |
| `Ctrl+a` depois `p` | Janela anterior |
| `Ctrl+a` depois `r` | Recarregar configuração |

### Comandos fora do tmux

```bash
tmux                      # Iniciar nova sessão
tmux new -s nome          # Criar sessão com nome
tmux ls                   # Listar sessões ativas
tmux attach -t nome       # Reconectar à sessão
tmux kill-session -t nome # Matar sessão específica
```

---

## 🛠️ Comandos Úteis

### eza (ls com ícones)

```bash
ls                            # Lista simples com ícones
ll                            # Lista detalhada com ícones
la                            # Mostra arquivos ocultos
lt                            # Visualização em árvore (2 níveis)
l                             # Lista completa com detalhes

# Comandos avançados
eza --icons -l --git          # Mostra status do git
eza --icons -l --sort=modified # Ordena por data modificação
eza --icons -l --sort=size    # Ordena por tamanho
eza --icons --tree --level=3  # Árvore com 3 níveis
```

### Zsh

```bash
source ~/.zshrc              # Recarregar configuração
nano ~/.zshrc                # Editar configuração
```

### Nano (editor de texto)

| Atalho | Ação |
|--------|------|
| `Ctrl+W` | Buscar texto |
| `Ctrl+\` | Buscar e substituir |
| `Ctrl+K` | Recortar linha |
| `Ctrl+U` | Colar |
| `Ctrl+O` | Salvar |
| `Ctrl+X` | Sair |

---

## 🐛 Troubleshooting

### Ícones aparecem como interrogações (?)

**Solução:** Verifique se a fonte Nerd Font está configurada:

1. Terminal → Preferências → Perfis → Texto
2. Fonte deve ser **MesloLGS NF**
3. Feche e abra o Terminal novamente

### Plugins não encontrados ao iniciar o terminal

**Erro:** `[oh-my-zsh] plugin 'zsh-autosuggestions' not found`

**Solução:** Reinstale os plugins:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### Tecla Option não funciona no tmux

**Solução:** Configure a tecla Option como Meta:

1. Terminal → Preferências → Teclado
2. Marque "Usar a tecla Option como tecla Meta"

### Warning sobre console output no Powerlevel10k

**Solução:** Execute:

```bash
p10k configure
```

### Atalhos do tmux não funcionam

**Verificar se está dentro do tmux:**

```bash
tmux
```

Você deve ver uma barra colorida na parte inferior.

---

## 🎨 Recursos Adicionais

- [Documentação Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)
- [Documentação Powerlevel10k](https://github.com/romkatv/powerlevel10k)
- [Documentação tmux](https://github.com/tmux/tmux/wiki)
- [Documentação eza](https://github.com/eza-community/eza)

---

## 📝 Notas

- **Mouse habilitado no tmux:** Você pode clicar nos painéis para trocar e redimensionar arrastando
- **Autocomplete:** Pressione `Tab` para autocompletar e `→` para aceitar sugestões
- **Histórico:** Use `Ctrl+R` para buscar no histórico de comandos

---

## ✅ Checklist Final

- [ ] Homebrew instalado
- [ ] Nerd Font instalada e configurada no Terminal
- [ ] Oh My Zsh instalado
- [ ] Powerlevel10k instalado e configurado
- [ ] Plugins instalados (autosuggestions, syntax-highlighting)
- [ ] tmux instalado e configurado
- [ ] eza instalado
- [ ] .zshrc configurado com aliases
- [ ] Tecla Option configurada como Meta
- [ ] `p10k configure` executado

---

**🎉 Pronto! Seu terminal está completo e estiloso!**

Criado em: Outubro 2025