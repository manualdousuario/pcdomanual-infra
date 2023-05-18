FROM freshrss/freshrss:1.21.0

# Remove Apache access logs
RUN sed -i 's/CustomLog \/dev\/stdout combined_proxy/CustomLog \/dev\/null combined_proxy/' /etc/apache2/sites-enabled/FreshRSS.Apache.conf