FROM odoo:9
MAINTAINER Eino Mäkitalo <eino.makitalo@avipartio.fi> 

# Allow sudo command with odoo user
USER root

RUN apt-get update && apt-get install -y sudo wget && rm -rf /var/lib/apt/lists/

RUN adduser odoo sudo && passwd -d odoo

RUN mkdir /var/lib/addons && mkdir /var/lib/addons/account_bank_statement_import_oko && \
    mkdir /var/lib/addons/l10n_fi_invoice && \
    mkdir /var/lib/addons/l10n_fi_scouts && \
    cd /var/lib/addons/account_bank_statement_import_oko && \
    wget -qO-   https://github.com/eino-makitalo/account_bank_statement_import_oko/tarball/9.0 | tar xvz --strip-components=1

RUN cd /var/lib/addons/l10n_fi_scouts && \
    wget -qO-  https://github.com/eino-makitalo/l10n_fi_scouts/tarball/9.0 | tar xvz --strip-components=1 

RUN cd /var/lib/addons/l10n_fi_invoice && \
    wget -qO- https://github.com/eino-makitalo/l10n_fi_invoice/tarball/refchange | tar xvz --strip-components=1

RUN chown -R odoo:odoo /var/lib/addons /var/lib/odoo

RUN sed -i 's|addons_path = |addons_path = /var/lib/addons,|' /etc/odoo/openerp-server.conf

USER odoo
