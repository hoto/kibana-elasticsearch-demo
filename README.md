# Kibana and Elasticsearch demo

Run:

    docker-compose up

    localhost:5601

Create kibana index in elasticsearch:

    curl

Create elasticsearch entry:

    curl

Reset and recreate the whole environment:

    docker-compose down -v
    docker-compose up

---

```bash
declare -A services
services[0]=service_a
services[1]=service_b
services[2]=service_c

declare -A severities
severities[0]=SEVERE 
severities[1]=ERROR 
severities[2]=WARN
severities[3]=INFO 
severities[4]=INFO 
severities[5]=INFO 
severities[6]=INFO 
severities[7]=INFO 
severities[8]=DEBUG
severities[9]=TRACE


for i in $(seq 1 100)
do
    randomService=${services[$[$RANDOM % ${#services[@]}]]}
    randomSeverity=${severities[$[$RANDOM % ${#severities[@]}]]}
    curl -X POST 'localhost:9200/production/services' \
        -H 'Content-Type: application/json' -d'
            {
            "serviceName" : "'${randomService}'",
            "serviceVersion" : "1.0.0",
            "message" : "Message from '${randomService}'",
            "severity" : "'${randomSeverity}'",
            "@timestamp" : "'$(date --utc +%FT%T)'"
            }
            ';
done
```

```
for i in $(seq 1 100);do echo ${severities[$[$RANDOM % ${#severities[@]}]]}; done | sort | uniq -c
```