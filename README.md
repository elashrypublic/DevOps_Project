1
Screenshot — App at https://localhost on Vm OR https://192.168.148.130

![alt text](<Screenshot 2026-03-06 191818.png>)


2
Screenshot — docker compose ps

![alt text](<Screenshot 2026-03-06 191911.png>)


3
Screenshot — curl /api/health

![alt text](<Screenshot 2026-03-06 192000.png>)


Architecture : 

![alt text](94eb5febd47d7d2fafbd8f507826a6639dae9089_2_690x388.png)



                ┌──────────────┐
                │    Client     │
                │  Browser/API  │
                └──────┬───────┘
                       │
                       ▼
               ┌──────────────┐
               │    NGINX     │
               │ ReverseProxy │
               │ LoadBalancer │
               └──────┬───────┘
                      │
        ┌─────────────┴─────────────┐
        ▼                           ▼
 ┌────────────┐              ┌────────────┐
 │  Flask1    │              │  Flask2    │
 │  Backend   │              │  Backend   │
 └─────┬──────┘              └─────┬──────┘
       │                           │
       ├──────────────┬────────────┤
       ▼              ▼            ▼
 ┌─────────┐    ┌──────────┐   ┌─────────┐
 │  Redis  │    │ Postgres │   │ pgAdmin │
 │  Cache  │    │ Database │   │ (tools) │
 └─────────┘    └──────────┘   └─────────┘

Networks:
- frontend
- backend

Volumes:
- pgdata
- redisdata