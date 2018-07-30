# Misc Notes

## Building the Docker Images
backend:
./build.sh
docker build -t dvonthenen/zop-backend .
docker push dvonthenen/zop-backend:latest

frontend:
./build.sh
docker build -t dvonthenen/zop-frontend .
docker push dvonthenen/zop-frontend:latest


## ScaleIO Clean Up
scli --login --username admin --password Scaleio123
scli --query_all_volumes
scli --unmap_volume_from_sdc --all_sdc --volume_name XXXXXX --i_am_sure
scli --remove_volume --volume_name XXXX

scli --mdm_ip 10.138.0.6 --add_volume --size_gb 32 --volume_name prometheus --protection_domain_name default --storage_pool_name default


## Random Debugging Stuff
docker ps --filter "status=exited" | awk '{print $1}' | xargs docker rm

docker run -ti --entrypoint=/bin/sh -p 9090:9090 prom/prometheus:v1.7.1

/bin/prometheus -config.file=/etc/prometheus/prometheus.yml -storage.local.path=/prometheus -web.console.libraries=/etc/prometheus/console_libraries -web.console.templates=/etc/prometheus/consoles

IMPORTANT: Dont forget to fix ports on GCE!!!!!
