## Reproduce the issue

### External

    curl  -k --limit-rate 800k  https://XXXXXXX/data/ea4761d6-c7b4-11ec-b6f4-01aa75ed71a1.en.PDF.pdf  -o /dev/null

### Inside a node

By using nsenter script (through the nodeport svc-nodeport.yaml).

    curl -k --limit-rate 800k https://localhost:30443/data/ea4761d6-c7b4-11ec-b6f4-01aa75ed71a1.en.PDF.pdf  -o /dev/null


