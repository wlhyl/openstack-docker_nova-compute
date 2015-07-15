# 环境变量
- KEYSTONE_ENDPOINT: keystone endpont
- RABBIT_HOST: rabbitmq IP
- RABBIT_USERID: rabbitmq user
- RABBIT_PASSWORD: rabbitmq user 的 password
- NOVA_PASS: openstack nova密码
- MY_IP: my_ip
- NOVNCPROXY_BASE_URL: novncproxy_base_url
- GLANCE_ENDPOINT: glance endpoint

# volumes:
- /opt/openstack/nova-cert/: /etc/nova
- /opt/openstack/log/nova-cert/: /var/log/nova/

# 启动nova-api
docker run -d --name nova-cert -p 8774:8774 \
    -v /opt/openstack/nova-cert/:/etc/nova \
    -v /opt/openstack/log/nova-cert/:/var/log/nova/ \
    -e NOVA_DB=10.64.0.52 \
    -e NOVA_DBPASS=nova_dbpass \
    -e RABBIT_HOST=10.64.0.52 \
    -e RABBIT_USERID=openstack \
    -e RABBIT_PASSWORD=openstack \
    -e KEYSTONE_ENDPOINT=10.64.0.52 \
    -e MY_IP=10.64.0.52 \
    -e GLANCE_ENDPOINT=10.64.0.52 \
    10.64.0.50:5000/lzh/nova-api:kilo