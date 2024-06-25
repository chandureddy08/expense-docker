FROM mysql:8.0

# Environment variables
ENV MYSQL_ROOT_PASSWORD=ExpenseApp@1 \
    MYSQL_USER=expense \
    MYSQL_PASSWORD=ExpenseApp@1 \
    MYSQL_DATABASE=transactions

# Copy initialization scripts
COPY scripts/*.sql /docker-entrypoint-initdb.d/

# Create a non-root user and group
RUN groupadd -r myusergroup && useradd -r -g myusergroup myuser

# Ensure the non-root user has permissions to the required directories and files
RUN mkdir -p /var/run/mysqld && \
    chown -R myuser:myusergroup /var/lib/mysql /var/run/mysqld /docker-entrypoint-initdb.d /etc/mysql

# Switch to the non-root user
USER myuser

# Expose port 3306
EXPOSE 3306

# Entrypoint
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["mysqld"]
