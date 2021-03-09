FROM docker.io/bitnami/redmine:4-debian-10

WORKDIR /opt/bitnami/redmine

RUN set -eux; \
    \
    apt-get update && apt-get install -y --no-install-recommends \
        subversion \
        subversion-tools \
    && rm -rf /var/lib/apt/lists/*; \
    chown -R bitnami:root .; \
    #unlink plugins; \
    #gosu bitnami:root mkdir plugins; \
    \
# install plugins
    gosu bitnami:root git config --global http.sslVerify false; \
    gosu bitnami:root git clone --depth 1 https://github.com/akiko-pusu/redmine_banner.git plugins/redmine_banner; \
    gosu bitnami:root git clone --depth 1 https://github.com/onozaty/redmine-view-customize.git plugins/view_customize; \
    gosu bitnami:root git clone --depth 1 https://github.com/haru/redmine_wiki_extensions.git plugins/redmine_wiki_extensions; \
    gosu bitnami:root git clone --depth 1 https://github.com/gtt-project/sidebar_hide.git plugins/sidebar_hide; \
    #gosu bitnami:root git clone --depth 1 https://gitlab.com/bdemirkir/sidebar_hide.git plugins/sidebar_hide; \
    #gosu bitnami:root git clone --depth 1 https://github.com/farend/scm-creator.git plugins/redmine_scm; \
    gosu bitnami:root git clone --depth 1 https://github.com/AlphaNodes/redmine_messenger.git plugins/redmine_messenger; \
    \
# install themes
    gosu bitnami:root git clone --depth 1 https://github.com/farend/redmine_theme_farend_basic.git public/themes/farend_basic; \
    gosu bitnami:root git clone -b redmine4.1 --depth 1 https://github.com/farend/redmine_theme_farend_bleuclair.git public/themes/bleuclair; \
    \
# install gems
    gosu bitnami:root bundle config unset deployment; \
    gosu bitnami:root bundle install;
