
## Helm и будущий Jenkins

- Хранить настройки окружения в Git: environments/dev-values.yaml.
- Перед использованием создать этот файл и явно задать параметры окружения.
- В Jenkins выполнять deploy с явными --reset-values и -f:
  helm upgrade --install demo ./charts/demo --kube-context k8s-lab -n demo --create-namespace --reset-values -f environments/dev-values.yaml --wait --timeout 5m
- --reset-values сбрасывает все сохранённые переопределения.
  Все необходимые настройки должны быть переданы текущим deploy.
- Причина правила: сохранённый --set replicaCount=2 перекрывал изменение
  values.yaml на 3; --reset-values устранил это.
- Проверять значения релиза через helm get values, результат — через kubectl.
  Новая ревизия Helm сама по себе не подтверждает нужное изменение.
- Основные команды и пояснения добавлять в корневой README.md.
- Секреты и kubeconfig в Git не сохранять.
- При переходе на Argo CD: Jenkins обновляет Git, Argo CD управляет deploy.
