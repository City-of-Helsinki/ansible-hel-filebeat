ansible-hel-filebeat
=========
Hello! This is a role for installing filebeat and using its modules
framework the get the logs flowing with minimum of fuss.

Modules in filebeat are prepackaged Filebeat configs & Elasticsearch
ingest pipeline setups. This makes ELK stack simpler, if somewhat
lackings in the L-department.

This role installs your chosen filebeat version (default is 7.1.x) and
enables your chosen modules. "system" is a good starting point, it ships out
/var/log/syslog & /var/log/auth.log out to elasticsearch.

Requirements
------------
Elasticsearch installation (or their cloud offering)
Ubuntu or Debian based server with logs to be shipped

Role Variables
--------------

```yaml
es_filebeat_es_hosts:
  - my.elk.server:9200
es_filebeat_modules:
  - name: module_i_want_to_use
    enabled: toggle_for_enabling_disabling_the_module
```

see defaults/main.yaml


Example Playbook
----------------

Install filebeat, have it send the system logs to Elasticsearch:

```yaml
  - hosts: all
    vars:
      es_filebeat_es_hosts:
        - my.elk.server:9200
      es_filebeat_modules:
        - name: system
          enabled: true
    roles:
      - role: ansible-hel-filebeat
```

License
-------
MIT

Author Information
------------------
Ville Koivunen @ hel.fi

based on roles elastic.elasticsearch & tbaczynski.filebeat
