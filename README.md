# SmartFlix TV Application

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![PySide6](https://img.shields.io/badge/GUI-PySide6-green.svg)](https://wiki.qt.io/Qt_for_Python)

SmartFlix TV é um aplicativo desktop completo para reprodução e gerenciamento de playlists M3U de IPTV e VODs (Vídeo On Demand). Desenvolvido com Python e PySide6, oferece uma experiência rica com múltiplos backends de reprodução e recursos avançados de gerenciamento de conteúdo.

## Índice
- [Recursos Principais](#recursos-principais)
- [Requisitos do Sistema](#requisitos-do-sistema)
- [Instalação e Uso](#instalação-e-uso)
- [Gestão de Playlist](#gestão-de-playlist)
- [Controle de Reprodução](#controle-de-reprodução)
- [Gerenciamento de Favoritos](#gerenciamento-de-favoritos)
- [Estrutura de Arquivos](#estrutura-de-arquivos)
- [Configurações Técnicas](#configurações-técnicas)

## Recursos Principais
✔️ **Backends de Reprodução:**  
- Suporte nativo para VLC (Windows) e Qt Multimedia (Linux)  
- Detecção automática do melhor player disponível  

✔️ **Gestão Inteligente de Playlists:**  
- Atualização automática de playlists remotas  
- Cache local com compactação gzip  
- Importação de arquivos locais (.m3u)  

✔️ **Sistema de Categorização:**  
- Agrupamento automático por categorias e padrões Série/Temporada  
- Ícones de logos automáticos com sistema de cache  

✔️ **Recursos Avançados:**  
- Marcador de progresso para VODs (assistidos / em progresso)  
- Barra de busca com filtro em tempo real  
- Sistema de favoritos persistemte para itens e séries  
- Controles de reprodução em tela cheia  

## Requisitos do Sistema
**Windows:**
```bash
pip install PySide6 requests python-vlc
```

**Linux:**
```bash
# Requer plugins GStreamer
sudo apt install gstreamer1.0-plugins-good gstreamer1.0-plugins-bad
pip install PySide6 requests
```

## Instalação e Uso
**Windows:**
- Faça o download e Execute o aplicativo: smart-flix-tv.exe

**Linux:**
- Faça o download e Execute o aplicativo: smart-flix-tv.appimage

⚙️ **Primeira execução:**
- Configure a URL da playlist em Arquivo > Configurações
- A playlist será automaticamente carregada e cacheada

**Gestão de Playlist:**

|Componente                     |Descrição                                        |
|-------------------------------|-------------------------------------------------|
|Atualização Remota             |Sincroniza lista via HTTP periodicamente         |
|Cache Local                    |Armazena playlist em playlist_cache.m3u.gz       |
|Estrutura em Árvore            |Organiza conteúdo por grupos e categorias        |
|Filtro Rápido                  |Busca em tempo real ao digitar na barra de busca |
|Estrutura em Árvore            |Organiza conteúdo por grupos e categorias        |

**Controle de Reprodução**
- Controles de play/pause/stop/volume integrados
- Seek slider para VODs com marcação temporal
- Modo fullscreen (tecla Esc para sair)
- Restauração automática de progresso em vídeos interrompidos
    
**Gerenciamento de Favoritos**
- ⭐ Ícone Estrela: Adiciona/remove itens ou séries inteiras
- Seção dedicada: Agrupa todos os favoritos no topo da lista
- Persistência: Salvo automaticamente em favorites.json

**Estrutura de Arquivos:**

|Arquivo                        |Função                                           |
|-------------------------------|-------------------------------------------------|
|settings.json                  |URL da playlist e configurações de atualização   |
|favorites.json                 |Itens e séries favoritadas pelo usuário          |
|playback_progress.json         |Status de reprodução de VODs                     |
|cache/logos/                   |Diretório de logos baixados (cache)              |
|playlist_cache.m3u.gz          |Playlist compactada em cache                     |

**Configurações Técnicas:**
```bash
# Configurações padrão (customizáveis via GUI)
default_settings = {
    "m3u_url": "http://exemplo.com/playlist.m3u",
    "update_interval_days": 3,
    "download_timeout_seconds": 60,
    "logo_cache_dir": "cache/logos"
}
```

**Fluxo de Reprodução:**
- Double-click em um item para iniciar reprodução
- Player seleciona backend apropriado (VLC/Qt)
- Para VODs, verifica progresso salvo anteriormente
- Offers opção de retomar ou reiniciar vídeos
     

**Sistemas Suportados:**
- Windows 10/11 (com VLC)
- Linux com QtMultimedia e GStreamer
- macOS (testes limitados)

**🚀 Futuras Implementações (Roadmap)**
-----------------------------------
*   **Internacionalização (i18n):** Preparar o aplicativo para ser traduzido para múltiplos idiomas (Português, Inglês, Espanhol).
    
*   **Melhorias na UI/UX:**
    
    *   Adicionar um menu de contexto (clique direito) nos itens da lista para ações rápidas (ex: "Adicionar/Remover dos Favoritos", "Marcar como assistido").
        
    *   Criar um painel de informações para exibir detalhes da mídia selecionada.
        
**🐞 Bugs e Problemas Conhecidos**
------------------------------

*   **VLC Portátil no Windows**
    
    *   **Descrição:** O executável .exe gerado pelo PyInstaller, mesmo contendo os arquivos do VLC, não consegue inicializar o player em uma máquina Windows que não tenha o VLC previamente instalado no sistema.
        
    *   **Status:** **Trabalho em andamento.**
        
    *   **Solução Temporária Adotada:** O VLC Media Player passa a ser um **requisito** para a utilização do SmartFlix TV na plataforma Windows.
        

💻 Requisitos de Execução
-------------------------

### Windows (10 / 11)

*   **Instalação do VLC Media Player:**
    
    *   **Obrigatório.** O aplicativo depende do VLC para decodificar e reproduzir vídeos.
        
    *   **Arquitetura:** A versão do VLC instalada no sistema deve ser a verão **64-bit**.
        
    *   **Download:** [Site Oficial do VideoLAN](https://www.videolan.org/vlc/)
        

### Linux

*   **Dependência Principal (Qt Multimedia):** GStreamer
    
*   O usuário precisa instalar os pacotes do GStreamer para que o QtMultimedia funcione. Os comandos variam conforme a distribuição:

*   Debian / Ubuntu / Derivados:

```bash
sudo apt update
sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-libav
```

*   Red Hat / Fedora / CentOS:

```bash
sudo dnf install gstreamer1-plugins-base gstreamer1-plugins-good gstreamer1-plugins-bad-free gstreamer1-plugins-ugly gstreamer1-libav
```

*   Arch Linux / Derivados:

```bash
sudo pacman -S gstreamer gst-plugins-base gst-plugins-good gst-plugins-bad gst-libav
```

## Baixar o Executável

A versão mais recente do aplicativo está disponível na aba [Releases](https://github.com/CarlosEduardoAraujo/SmartFlixTV-PC/releases).

## Suporte e Feedback

Se você encontrar algum problema ou tiver sugestões de melhoria, por favor abra uma [Issue](https://github.com/CarlosEduardoAraujo/SmartFlixTV-PC/issues). Se quiser falar diteramente, entre em nosso Discord e interaja https://discord.gg/XPGMh2UmE6. A comunidade e os desenvolvedores estão prontos para ajudar.

## Listas IPTV

Nós não distribuimos lista IPTV*

Desenvolvido para entusiastas de IPTV! 
