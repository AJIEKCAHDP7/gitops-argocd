# GitOps AСrgoCD - Работа с ArgoCD

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

Установка ArgoCD
 Создание namespace:
 kubectl create namespace argocd
 Установка ArgoCD:
 kubectl apply -n argocd -f 
https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
 Просмотр состояния Pod:
 kubectl get pods -n argocd
 Проброс портов:
 kubectl port-forward svc/argocd-server -n argocd 8080:443
 Получение пароля администратора:
 kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d



1. Создание репозитория в gitLabs.
