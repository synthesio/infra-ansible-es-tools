# Elasticsearch Tools

This is a set of tasks we use to manage an Elasticsearch cluster.

Available tasks are:

- create an index,
- optimize a whole cluster, starting with the index having the greatest number of deleted documents,
- optimize an index,
- enable / disable rack awareness,
- perform a rolling restart,
- include / exclude a rack, zone or a set of hosts,
- update an index or a cluster refresh time,
- update an index or a cluster number of replicas.

We use a set of variables for all our clusters:

- `rack_id`: the rack name for rack awareness.
- `cluster_addr`: by default, the host you'll target with the role
- `es_version`: Elasticsearch version, 1, 2 or 5

## Create an index

```
ansible-playbook -i inventory -l host -e task=create_index -e index_name [ -e shards=number_of shards -e replicas=number_of_replicas] playbooks/ops_es_tools.yml
```

## Optimize a cluster

```
ansible-playbook -i inventory -l host -e task=optimize_cluster -e es_version={1,2,5} playbooks/ops_es_tools.yml
```

## Optimize an index

```
ansible-playbook -i inventory -l host -e task=optimize_index -e es_version={1,2,5} -e index=index_name playbooks/ops_es_tools.yml
```

## Rolling restart

```
ansible-playbook -i inventory -l cluster -e task=rolling_restart -e rack=foo playbooks/ops_es_tools.yml
ansible-playbook -i inventory -l cluster -e task=rolling_restart -e rack=bar playbooks/ops_es_tools.yml
```

## Routing allocation

```
ansible-playbook -i inventory -l host -e task=routing_allocation -e index=index_name -e action={enable,disable} -e what={rack,zone,_ip} -e value="some,thing,or,nothing" playbooks/ops_es_tools.yml
```

## Update refresh time

```
ansible-playbook -i inventory -l host -e task=update_refresh_time -e refresh_time=60s playbooks/ops_es_tools.yml
```

## Update the number of replicas

```
ansible-playbook -i inventory -l host -e task=update_replicas -e replicas=42 [-e index=index_name] playbooks/ops_es_tools.yml
```
