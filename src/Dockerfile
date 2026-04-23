FROM kasmweb/ubuntu-focal-desktop:1.15.0
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME

######### Customize Container Here ###########

RUN apt update && apt -y upgrade

# Core utilities
RUN apt -y install \
    openvpn \
    unzip \
    curl \
    wget \
    git \
    jq \
    fzf \
    bat \
    ripgrep \
    fd-find \
    htop \
    tree \
    nmap \
    netcat \
    dnsutils \
    whois \
    direnv

# Change Background to xcad wallpaper
COPY assets/mr-robot-wallpaper.png /usr/share/extra/backgrounds/bg_default.png

# ── Starship ──────────────────────────────────────────────────────────────────
RUN curl -sS https://starship.rs/install.sh | sh -s -- -y

# Add Starship to bashrc
RUN echo 'eval "$(starship init bash)"' >> .bashrc

# Add updated Starship config (xcad dotfiles version)
COPY config/starship.toml .config/starship.toml

# ── Hack Nerd Font v3 ─────────────────────────────────────────────────────────
RUN wget -q https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/Hack.zip \
    && unzip -q Hack.zip -d /usr/local/share/fonts/HackNerdFont \
    && rm Hack.zip \
    && fc-cache -fv

# ── eza (modern ls replacement) ───────────────────────────────────────────────
RUN wget -q https://github.com/eza-community/eza/releases/latest/download/eza_x86_64-unknown-linux-gnu.tar.gz \
    && tar -xzf eza_x86_64-unknown-linux-gnu.tar.gz \
    && mv eza /usr/local/bin/eza \
    && rm -f eza_x86_64-unknown-linux-gnu.tar.gz

# ── zoxide (smarter cd) ───────────────────────────────────────────────────────
RUN curl -sS https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | bash \
    && echo 'eval "$(zoxide init bash)"' >> .bashrc

# ── Shell aliases (from xcad dotfiles) ───────────────────────────────────────
RUN printf '\n# xcad aliases\nalias ls="eza --icons --group-directories-first"\nalias ll="eza --icons --group-directories-first -l"\nalias la="eza --icons --group-directories-first -la"\nalias cat="batcat"\nalias fd="fdfind"\n' >> .bashrc

# ── direnv hook ───────────────────────────────────────────────────────────────
RUN echo 'eval "$(direnv hook bash)"' >> .bashrc

# ── Terminator with xcad color theme ─────────────────────────────────────────
RUN apt -y install terminator
RUN mkdir -p .config/terminator
COPY config/terminator.toml .config/terminator/config

# ── Warp terminal theme ───────────────────────────────────────────────────────
RUN mkdir -p .warp/themes
COPY config/warp/xcad2k-dark.yml .warp/themes/xcad2k-dark.yml
COPY config/warp/keybindings.yaml .warp/keybindings.yaml

# ── XFCE Dark Theme ───────────────────────────────────────────────────────────
RUN apt install -y numix-gtk-theme numix-icon-theme

######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME

USER 1000
