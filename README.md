# Домашнее задание к занятию «Введение в Terraform»
------
### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии >=1.8.4 . Приложите скриншот вывода команды ```terraform --version```.
2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.
3. Убедитесь, что в вашей ОС установлен docker.

Решение:  
Устанавливаем согласно документации с официально сайта, с использованием менеджера пакетов apt, при подлюченном VPN (для обхода региональных ограничений) 
![Screen_1](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/1-1.jpg)
![Screen_2](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/1.jpg)

### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте.
Решение: Файлы скопированы

3. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)  
Решение: Хранение в файле personal.auto.tfvars  
![Screen_3](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/2.jpg)

4. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.  
Решение:  
![Screen_4](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/3.jpg)

5. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.
Решение:  
При первоначальном выполнении получем 2 ошибки:  
![Screen_5](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/4-1.jpg)  
Отсутсвует уникальное имя (name) при описании ресурса docker_image  

![Screen_6](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/4-2.jpg)  
Уникальное имя ресурса (name) не может начинаться с цифры.

После исправления, последовательно получаме еще 2 ошибки:  
![Screen_7](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/4-3.jpg)  
Неверно указнный параметр random.string.FAKE. Не соответсвует описанию ресурса random_password.  

![Screen_8](https://github.com/ArtWander/Terra/blob/333bcfe832ecaad892b0752b0253571866c3fd76/img/4-4.jpg)  
Неверно указнный атрибут random_string.resulT. Регистр символов критичен. Решение подсказвает сама система.  

Итоговый исправленный код:  
![Screen_9](https://github.com/ArtWander/Terra/blob/4dc594a046050bd3b7e18d1e28e5e0317a75b284/img/4-5.jpg)  

6. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.  
Решение:
![Screen_10](https://github.com/ArtWander/Terra/blob/4dc594a046050bd3b7e18d1e28e5e0317a75b284/img/4-6.jpg)  

7. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.
Решение:  
![Screen_11](https://github.com/ArtWander/Terra/blob/4dc594a046050bd3b7e18d1e28e5e0317a75b284/img/4-7.jpg)
Ключ ```-auto-approve``` используется для выполнения плана без ручного подтверждения. Исключает возможность просмотреть изменения до их применения. Может привести к непреднамеренным изменениям в инфраструктуре.
Используется для автоматизации процесса развертывания. Он больше подходит для сред разработки или тестирования, где распространены быстрые итерации и влияние изменений ниже.  

9. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**.
Решение:  
![Screen_12](https://github.com/ArtWander/Terra/blob/f0677a6f02a4aa6b20861c0ea79ba75fe1bf2a0e/img/4-8.jpg)

10. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации
Решение:
В описании ресурса docker_image использован параметр keep_locally = true.  
![Screen_13](https://github.com/ArtWander/Terra/blob/68bdba1475cf34e089e6a01558763441be8fd7c7/img/4-9.jpg)
    

### Задание 3*
1. Установите [opentofu](https://opentofu.org/)(fork terraform с лицензией Mozilla Public License, version 2.0) любой версии
2. Попробуйте выполнить тот же код с помощью ```tofu apply```, а не terraform apply.  
Решение:

![Screen_14](https://github.com/ArtWander/Terra/blob/2d0cdf3063a0b467a3d6cf8e02e8e5e15f4dcba5/img/6-1.jpg)
![Screen_15](https://github.com/ArtWander/Terra/blob/2d0cdf3063a0b467a3d6cf8e02e8e5e15f4dcba5/img/6-2.jpg)
   
