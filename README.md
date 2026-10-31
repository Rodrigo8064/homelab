# homelab
 
Infraestrutura do meu servidor: Traefik (proxy reverso / load balancer) + stacks das aplicações.
 
## Layout esperado (repos lado a lado)
 
~/projetos/
├── homelab/                 <- este repo
│   ├── traefik/
│   └── homepage/
└── portfolio-homepage/      <- repo do código do site (Dockerfile mora lá)
 
O compose da homepage usa `context: ../../portfolio-homepage`,
então os dois repos precisam estar na mesma pasta pai, com esses nomes.
 
## Clonar (notebook ou servidor)
 
mkdir -p ~/projetos && cd ~/projetos
git clone <url-do-homelab>
git clone <url-do-portfolio-homepage>
 
## Subir
 
cd ~/projetos/homelab/traefik  && docker compose up -d
cd ~/projetos/homelab/homepage && BUILDX_BAKE_ENTITLEMENTS_FS=0 docker compose up -d --build
 
## Testar (sem Cloudflare)
 
curl -H "Host: rodrigoolima.com.br" http://localhost/
 
## Debug
 
docker logs -f traefik
docker compose ps        # homepage deve ficar "healthy"
 
