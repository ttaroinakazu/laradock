ARG COOKIE_VALUE=HelloWorld
FROM rabbitmq:3.11-alpine

LABEL maintainer="Mahmoud Zalt <mahmoud@zalt.me>"

ARG COOKIE_VALUE=$COOKIE_VALUE

RUN rabbitmq-plugins enable --offline rabbitmq_management

RUN printf 'log.console = true\nlog.console.level = warning\nlog.default.level = warning\nlog.connection.level = warning\nlog.channel.level = warning\nlog.file.level = warning\n' > /etc/rabbitmq/conf.d/10-logs_to_stdout.conf && \
    printf 'loopback_users.guest = false\n' > /etc/rabbitmq/conf.d/20-allow_remote_guest_users.conf && \
    printf 'management_agent.disable_metrics_collector = true' > /etc/rabbitmq/conf.d/30-disable_metrics_data.conf && \
    chown rabbitmq:rabbitmq /etc/rabbitmq/conf.d/* && mkdir -p /var/lib/rabbitmq/ && \
    echo "$COOKIE_VALUE" > /var/lib/rabbitmq/.erlang.cookie && chmod 400 /var/lib/rabbitmq/.erlang.cookie && \
    chown -R rabbitmq:rabbitmq /var/lib/rabbitmq

EXPOSE 4369 5671 5672 15671 15672 25672
