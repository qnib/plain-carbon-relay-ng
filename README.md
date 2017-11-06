# plain-carbon-relay-ng
Plain image holding carbon-relay-ng

**Version**: v1

## Fire up

```bash
$ docker stack deploy -c docker-compose.yml carbon-relay-ng
Creating service carbon-relay-ng_relay
Creating service carbon-relay-ng_backend
Creating service carbon-relay-ng_chronograf
Creating service carbon-relay-ng_frontend
$ docker service ls
ID                  NAME                         MODE                REPLICAS            IMAGE                                                                                         PORTS
wvfvt8x18ctq        carbon-relay-ng_backend      replicated          1/1                 qnib/plain-influxdb@sha256:562d863843c48700b6d8d84c953ad86080b109c598e488733639c2d5cce7df65   *:8083->8083/tcp,*:8086->8086/tcp
4k64q28mcdnw        carbon-relay-ng_chronograf   replicated          1/1                 qnib/plain-chronograf:0.1.3.7                                                                 *:8888->8888/tcp
ys89x9nf7gy5        carbon-relay-ng_frontend     replicated          1/1                 qnib/plain-grafana4:4.5.2                                                                     *:3000->3000/tcp
eluirbxwdp4a        carbon-relay-ng_relay        replicated          1/1                 qnib/plain-carbon-relay-ng:latest                                                             *:2003->2003/tcp,*:2004->2004/tcp,*:8081->8081/tcp
$
```

Send metrics to the relay:

```bash
$ for x in {1..100};do echo "test ${RANDOM} $(date +%s)" |nc localhost 2003;sleep 5;done
```
