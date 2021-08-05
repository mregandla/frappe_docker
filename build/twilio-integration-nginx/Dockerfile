FROM bitnami/node:12-prod

COPY build/twilio-integration-nginx/install_app.sh /install_app

RUN /install_app twilio-integration https://github.com/frappe/twilio-integration master

FROM frappe/erpnext-nginx:edge

COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync
RUN echo -n "\ntwilio-integration" >> /var/www/html/apps.txt

VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
