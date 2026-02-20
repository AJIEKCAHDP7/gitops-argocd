# GitOps ArgoCD - Работа с ArgoCD

ArgoCD – это декларативный инструмент GitOps для непрерывной доставки (Continuous Delivery) в 
Kubernetes. Он автоматизирует развертывание приложений, синхронизируя состояние 
кластера с описанием в Git-репозитории.

Для чего нужен Argo CD?
 ● Автоматизация деплоя: Устраняет ручное управление развертыванием через kubectl 
или Helm.
 ● Синхронизация состояний: Следит за расхождениями между Git и кластером, 
автоматически исправляя их (self-healing).
 ● Мультикластерное управление: Работает с несколькими кластерами (dev, staging, 
production) одновременно.
 ● Безопасность и аудит: Все изменения проходят через Git, что обеспечивает контроль 
версий и прозрачность .
 ● Поддерживает популярные форматы конфигураций Kubernetes(Kubernetes-манифесты, 
Helm) 

# Установка ArgoCD

1. Создание namespace:
 kubectl create namespace argocd
2. Установка ArgoCD:
 kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
3. Просмотр состояния Pod:
 kubectl get pods -n argocd
4. Проброс портов:
 kubectl port-forward svc/argocd-server -n argocd 8080:443
5. Получение пароля администратора:
 kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
6. Создание репозитория в gitLabs.
7. Добавление публичного ключа Preferences - GitLab.
8. Клонируем репозиторий git clone ....
9. Установка утилиты ArgoCD
    
 # Для Linux
 curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
 sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
 rm argocd-linux-amd64

 10. Аутентификация:
 argocd login <ARGOCD_SERVER_IP> --username admin

 11. Добавление репозитория в ArgoCD:

Для публичного репозитория: 
argocd repo add https://github.com/argoproj/argocd-example-apps
 Для приватного репозитория: 
argocd repo add https://github.com/your-username/private-repo.git 
\ --username <username> 
\ --password <token-or-password> 
С SSH-ключом: 
argocd repo add git@github.com:your-username/repo.git \ --ssh-private-key-path ~/.ssh/id_rsa 
Проверить список репозиториев: 
argocd repo list

12. В репозитории создаем манифест с апликейшином, пример nginx Deployment.yaml с Service
13. git status + git add . -A
14. git commit -m "Add deployment...."
15. git push
16. Добавляем и редактируем app.yaml
17. Добавление манифеста: kubectl create -f app.yaml
18. Подхватывается и разварачивается Deployment
19. Ручная синхронизация приложения(если отключена автоматическая в манифесте): argocd app sync app
20. Проверка статуса: argocd app get app
21. Список всех приложений: argocd app lis
    
