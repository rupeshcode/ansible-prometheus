# Ansible Role: Prometheus Exporters
An ansible role which contains multiple exporters of prometheus for scrapping data and for enhancing your monitoring stack. Here are the list of exporters which we are supporting in this role:-
- **[Apache Exporter](https://github.com/Lusitaniae/apache_exporter)**
- **[Elasticsearch Exporter](https://github.com/justwatchcom/elasticsearch_exporter)**
- **[MongoDB Exporter](https://github.com/dcu/mongodb_exporter)**
- **[MySQL Exporter](https://github.com/prometheus/mysqld_exporter)**
- **[Nginx Exporter](https://github.com/nginxinc/nginx-prometheus-exporter)**
- **[Node Exporter](https://github.com/prometheus/node_exporter)**
## Requirments
For **[MySQL Exporter](https://github.com/prometheus/mysqld_exporter)**, Create a user in mysql with these privileges
```sql
CREATE USER 'exporter'@'localhost' IDENTIFIED BY 'password';
GRANT PROCESS, REPLICATION CLIENT,
SELECT ON *.* TO 'exporter'@'localhost' WITH MAX_USER_CONNECTIONS 3;
FLUSH PRIVILEGES;
```
---
For **[Nginx Exporter](https://github.com/nginxinc/nginx-prometheus-exporter)**, We have to enable **stub_status** in nginx configuration. In your Nginx Conf add this line to your **location** block
```conf
location / {
    stub_status on;
}
```

## Role Variables
### Mandatory Variables
**Needs to be change depending upon environment**

|**Variables**| **Default Values**| **Description**|
|----------|---------|---------------|
|**node_exporter_version** | 0.17.0 | Version of Node Exporter|
|**apache_exporter** | 0.5.0 | Version of Apache Exporter|
|**es_exporter** | 1.0.2 | Version of Elasticsearch Exporter|
|**mongodb_exporter** | 1.0.0 | Version of MongoDB Exporter|
|**nginx_exporter** | 0.2.0 | Version of Nginx Exporter|
|**mysql_exporter_version** | 0.11.0 | Version of MySQL Exporter|

## Dependencies
None :-)

## Example Playbook
Here is an example playbook:-
```yml
---
- hosts: exporter
  user: ubuntu
  become: yes
  roles:
    - name.ansible-role-prometheus-exporters
```

## Usage
For using this role you have to pass one variable to role which is **exporter_name**
```shell
ansible-playbook -i hosts site.yml -e exporter_name="node"
```
For running multiple exporter on same host you can use
```shell
ansible-playbook -i hosts site.yml -e exporter_name=["node", "apache"]
```

Values of **exporter_name** could be:-

|**Values** | **Description** |
|-----------|----------|
|**node** | For Node Exporter |
|**mysql** | For MySQL Exporter |
|**apache** | For Apache Exporter |
|**mongodb** | For MongoDB Exporter |
|**nginx** | For Nginx Exporter |
|**elasticsearch** | For Elasticsearch Exporter |
