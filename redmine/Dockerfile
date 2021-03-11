FROM docker.io/bitnami/redmine:4-debian-10

WORKDIR /opt/bitnami/redmine

COPY vendor/cache/* vendor/cache/

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
    gosu bitnami:root git clone --depth 1 https://github.com/redmica/redmine_issues_panel.git plugins/redmine_issues_panel; \
    gosu bitnami:root git clone --depth 1 https://github.com/AlphaNodes/redmine_messenger.git plugins/redmine_messenger; \
    #gosu bitnami:root git clone --depth 1 https://github.com/farend/scm-creator.git plugins/redmine_scm; \
    gosu bitnami:root git clone --depth 1 https://github.com/haru/redmine_wiki_extensions.git plugins/redmine_wiki_extensions; \
    gosu bitnami:root git clone --depth 1 https://github.com/gtt-project/sidebar_hide.git plugins/sidebar_hide; \
    #gosu bitnami:root git clone --depth 1 https://gitlab.com/bdemirkir/sidebar_hide.git plugins/sidebar_hide; \
    gosu bitnami:root git clone --depth 1 https://github.com/onozaty/redmine-view-customize.git plugins/view_customize; \
    \
# install themes
    gosu bitnami:root git clone -b redmine4.1 --depth 1 https://github.com/farend/redmine_theme_farend_bleuclair.git public/themes/bleuclair; \
    gosu bitnami:root git clone --depth 1 https://github.com/farend/redmine_theme_farend_basic.git public/themes/farend_basic; \
    \
# install gems
    gosu bitnami:root bundle config unset deployment; \
    gosu bitnami:root bundle install --local --no-cache;

ENV SESSION_KEY_SUFFIX=""

RUN set -eux; \
    \
    sed -i -r "s/(:filter_html => true)/#\1/" lib/redmine/wiki_formatting/markdown/formatter.rb; \
    sed -i -r "s/(:key => '_redmine_session')/\1 + ENV['SESSION_KEY_SUFFIX']/" config/application.rb;
