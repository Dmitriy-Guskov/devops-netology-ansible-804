# Домашнее задание к занятию "8.4 Работа с Roles"

## Подготовка к выполнению
1. Создайте два пустых публичных репозитория в любом своём проекте: kibana-role и filebeat-role.
2. Добавьте публичную часть своего ключа к своему профилю в github.

## Основная часть

Наша основная цель - разбить наш playbook на отдельные roles. Задача: сделать roles для elastic, kibana, filebeat и написать playbook для использования этих ролей. Ожидаемый результат: существуют два ваших репозитория с roles и один репозиторий с playbook.

1. Создать в старой версии playbook файл `requirements.yml` и заполнить его следующим содержимым:
   ```yaml
   ---
     - src: git@github.com:netology-code/mnt-homeworks-ansible.git
       scm: git
       version: "2.0.0"
       name: elastic 
   ```
2. При помощи `ansible-galaxy` скачать себе эту роль.
3. Создать новый каталог с ролью при помощи `ansible-galaxy role init kibana-role`.
4. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 
5. Перенести нужные шаблоны конфигов в `templates`.
6. Создать новый каталог с ролью при помощи `ansible-galaxy role init filebeat-role`.
7. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 
8. Перенести нужные шаблоны конфигов в `templates`.
9. Описать в `README.md` обе роли и их параметры.
10. Выложите все roles в репозитории. Проставьте тэги, используя семантическую нумерацию.
11. Добавьте roles в `requirements.yml` в playbook.
12. Переработайте playbook на использование roles.
13. Выложите playbook в репозиторий.
14. В ответ приведите ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.


Создал два репозитория
  - src: git@github.com:Dmitriy-Guskov/kibana-role.git
    version: "2.0.1"
  - src: git@github.com:Dmitriy-Guskov/filebeat-role.git
    version: "2.0.0"

Развернул 3 виртуалки в Яндексе
   -  elastic001
   -  kibana001
   -  filebeat001

Playbook создан, результат работы:



```
derpanter@Panters-MBP15 devops-netology-ansible-804 % ansible-galaxy install -r requirements.yml -p roles
Starting galaxy role install process
- elastic (2.0.0) is already installed, skipping.
- extracting kibana to /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/kibana
- kibana (2.0.1) was installed successfully
- extracting filebeat to /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/filebeat
- filebeat (2.0.0) was installed successfully
derpanter@Panters-MBP15 devops-netology-ansible-804 % 
```




```

derpanter@Panters-MBP15 devops-netology-ansible-804 % ansible-playbook -i inventory/hosts.yml site.yml --diff

PLAY [Assert elastic] **************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [elastic001]

TASK [elastic : Fail if unsupported system detected] *******************************************************************************
skipping: [elastic001]

TASK [elastic : include_tasks] *****************************************************************************************************
included: /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/elastic/tasks/download_yum.yml for elastic001

TASK [elastic : Download Elasticsearch's rpm] **************************************************************************************
ok: [elastic001 -> localhost]

TASK [elastic : Copy Elasticsearch to managed node] ********************************************************************************
ok: [elastic001]

TASK [elastic : include_tasks] *****************************************************************************************************
included: /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/elastic/tasks/install_yum.yml for elastic001

TASK [elastic : Install Elasticsearch] *********************************************************************************************
ok: [elastic001]

TASK [elastic : Configure Elasticsearch] *******************************************************************************************
ok: [elastic001]

PLAY [Assert kibana] ***************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [kibana001]

TASK [kibana : Fail if unsupported system detected] ********************************************************************************
skipping: [kibana001]

TASK [kibana : include_tasks] ******************************************************************************************************
included: /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/kibana/tasks/download_yum.yml for kibana001

TASK [kibana : Download kibana's rpm] **********************************************************************************************
ok: [kibana001 -> localhost]

TASK [kibana : Copy kibana to managed node] ****************************************************************************************
ok: [kibana001]

TASK [kibana : include_tasks] ******************************************************************************************************
included: /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/kibana/tasks/install_yum.yml for kibana001

TASK [kibana : Install kibana] *****************************************************************************************************
ok: [kibana001]

TASK [kibana : Configure Kibana] ***************************************************************************************************
ok: [kibana001]

PLAY [Assert filebeat] *************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [filebeat001]

TASK [filebeat : Fail if unsupported system detected] ******************************************************************************
skipping: [filebeat001]

TASK [filebeat : include_tasks] ****************************************************************************************************
included: /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/filebeat/tasks/download_yum.yml for filebeat001

TASK [filebeat : Download filebeat's rpm] ******************************************************************************************
ok: [filebeat001 -> localhost]

TASK [filebeat : Copy filebeat to managed node] ************************************************************************************
ok: [filebeat001]

TASK [filebeat : include_tasks] ****************************************************************************************************
included: /Users/derpanter/devops-netology-ansible-804/devops-netology-ansible-804/roles/filebeat/tasks/install_yum.yml for filebeat001

TASK [filebeat : Install filebeat] *************************************************************************************************
ok: [filebeat001]

TASK [filebeat : Configure filebeat] ***********************************************************************************************
ok: [filebeat001]

PLAY RECAP *************************************************************************************************************************
elastic001                 : ok=7    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
filebeat001                : ok=7    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
kibana001                  : ok=7    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
```