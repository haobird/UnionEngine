FROM mysql:5.6

# Write Permission
RUN usermod -u 1000 mysql && chown mysql.mysql /var/run/mysqld/

# Add image configuration and scripts
ADD build/run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

CMD ["/usr/local/bin/run"]
