1. Edit `inventories\hosts.ini.example file (remove .example)`:
```bash
[prometheus_server]
localhost ansible_connection=local

[remote_nodes]
your_server1 ansible_user=rewxrld
your_server2 ansible_user=rewxrld
your_server3 ansible_user=rewxrld
```

2. Edit `roles\prometheus\files\prometheus.yml`:
```bash
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporters'
    static_configs:
      - targets:
          - 'your_server1:9100'
          - 'your_server2:9100'
          - 'your_server3:9100'
```

3. Setup playbook with:
`ansible-playbook -i inventories\hosts.ini setup-monitoring.yml --ask-became-pass`
