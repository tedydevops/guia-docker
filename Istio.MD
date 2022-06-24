# como fazer funcionar Istio num cluster?
1) download e install
2) criar o control plane do istio no control plane do kubernetes: 
 $ istioclt install
3) para inserir proxys do istio nos PODs, é preciso criar um LABEL no namespace, e nao pode haver nenhum LABELS nele, verifique e entao crie o LABEL:
 $ k get ns deafult --show-labels  
 $ k label namespace default istio-injection=enabled
4) se houver PODs já criados é necessarios apaga-los pelo manifesto e recria-los:
 $ k delete -f <manifesto.yaml>
 $ k apply -f <manifesto.yaml>
5) é possivel ver que haverá um POD extra por container, contendo os proxys do istio:
 $ k get po
 
 # como visualizar/manejar metrics advindos desses proxys dos PODs:
 1) procurar e dar apply no path do istio baixado na pasta istio-<versão>/samples/addons desejados (pode ser grafana, prometheus,...), ex:
 $ k apply -f istio-<versão>/samples/addons/grafana.yaml
  se ja estiver na pasta após dar cd no path:
 $ k apply -f prometheus.yaml 
 2) para acessar prometheus, vai colocar a PORT mostrada no $k get svc -n istio-system :
 $ k port-forward svc/prometheus -n istio-system 9090
  - vai mostrar um "Forwarding from <ip:port> -> port"
  - no caso do prometheus: "Forwarding from <ip:9090> -> 9090"
 3) colar esse <ip:port> no navegador
