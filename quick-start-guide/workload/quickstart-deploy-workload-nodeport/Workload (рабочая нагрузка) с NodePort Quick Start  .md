



**Необходимое условие**

У вас есть работающий кластер как минимум с 1 нодой.

**1. Развертывание рабочей нагрузки**

Вы готовы создать свою первую Workload (рабочую [нагрузку](https://kubernetes.io/docs/concepts/workloads/ "https://kubernetes.io/docs/concepts/workloads/")) Kubernetes . Workload — это объект, который включает модули вместе с другими файлами и информацией, необходимой для развертывания вашего приложения.

Для этой рабочей нагрузки вы будете развертывать приложение Rancher Hello-World.

1. Щелкните **☰ > Управление кластером** .
1. На странице « **Кластеры** » перейдите к кластеру, в котором должна быть развернута рабочая нагрузка, и нажмите « **Исследовать** » .
1. Щелкните **Рабочая нагрузка** .
1. Щелкните **Создать** .
1. Введите **имя** для вашей рабочей нагрузки.
1. В поле **Container Image - Образ контейнера** введите rancher/hello-world. Это поле чувствительно к регистру.
1. Щелкните **Добавить порт** .
1. В раскрывающемся списке «**Service Type -** **Тип службы** » убедитесь, что выбран **NodePort** . <https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/img/rancher/nodeport-dropdown.png> 
1. В поле **Publish the container port - Опубликовать порт контейнера** введите порт 80.  <https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/img/rancher/container-port-field.png>
1. Щелкните **Create - Создать** .

**Результат:**

- Ваша рабочая нагрузка развернута. Этот процесс может занять несколько минут.
- Когда ваша рабочая нагрузка завершает развертывание, ей присваивается состояние **Active** . Вы можете просмотреть этот статус на странице **Workloads -** **рабочих нагрузок** проекта .



**2. Просмотр вашего приложения**

На странице « **Workloads - Рабочие нагрузки** » щелкните ссылку под своей рабочей нагрузкой. Если ваше развертывание прошло успешно, ваше приложение откроется.

**Внимание: Sandboxes -  облачные песочницы**

При использовании виртуальной машины, размещенной в облаке, у вас может не быть доступа к порту, на котором запущен контейнер. В этом случае вы можете протестировать Nginx в сеансе ssh на локальном компьютере, используя файлы Execute Shell. Используйте номер порта после **:** в ссылке вашей рабочей нагрузки, если он доступен, как 31568в этом примере.



gettingstarted@rancher:~$ curl http://localhost:31568

<!DOCTYPE html>

<html>

`  `<head>

`    `<title>Rancher</title>

`    `<link rel="icon" href="img/favicon.png">

`    `<style>

`      `body {

`        `background-color: white;

`        `text-align: center;

`        `padding: 50px;

`        `font-family: "Open Sans","Helvetica Neue",Helvetica,Arial,sans-serif;

`      `}

`      `button {

`          `background-color: #0075a8;

`          `border: none;

`          `color: white;

`          `padding: 15px 32px;

`          `text-align: center;

`          `text-decoration: none;

`          `display: inline-block;

`          `font-size: 16px;

`      `}



`      `#logo {

`        `margin-bottom: 40px;

`      `}

`    `</style>

`  `</head>

`  `<body>

`    `<img id="logo" src="img/rancher-logo.svg" alt="Rancher logo" width=400 />

`    `<h1>Hello world!</h1>

`    `<h3>My hostname is hello-world-66b4b9d88b-78bhx</h3>

`    `<div id='Services'>

`      `<h3>k8s services found 2</h3>



`      `<b>INGRESS\_D1E1A394F61C108633C4BD37AEDDE757</b> tcp://10.43.203.31:80<br />



`      `<b>KUBERNETES</b> tcp://10.43.0.1:443<br />



`    `</div>

`    `<br />



`    `<div id='rancherLinks' class="row social">

`      `<a class="p-a-xs" href="https://rancher.com/docs"><img src="img/favicon.png" alt="Docs" height="25" width="25"></a>

`      `<a class="p-a-xs" href="https://slack.rancher.io/"><img src="img/icon-slack.svg" alt="slack" height="25" width="25"></a>

`      `<a class="p-a-xs" href="https://github.com/rancher/rancher"><img src="img/icon-github.svg" alt="github" height="25" width="25"></a>

`      `<a class="p-a-xs" href="https://twitter.com/Rancher\_Labs"><img src="img/icon-twitter.svg" alt="twitter" height="25" width="25"></a>

`      `<a class="p-a-xs" href="https://www.facebook.com/rancherlabs/"><img src="img/icon-facebook.svg" alt="facebook" height="25" width="25"></a>

`      `<a class="p-a-xs" href="https://www.linkedin.com/groups/6977008/profile"><img src="img/icon-linkedin.svg" height="25" alt="linkedin" width="25"></a>

`    `</div>

`    `<br />

`    `<button class='button' onclick='myFunction()'>Show request details</button>

`    `<div id="reqInfo" style='display:none'>

`      `<h3>Request info</h3>

`      `<b>Host:</b> 172.22.101.111:31411 <br />

`      `<b>Pod:</b> hello-world-66b4b9d88b-78bhx </b><br />



`      `<b>Accept:</b> [\*/\*]<br />



`      `<b>User-Agent:</b> [curl/7.47.0]<br />



`    `</div>

`    `<br />

`    `<script>

`      `function myFunction() {

`          `var x = document.getElementById("reqInfo");

`          `if (x.style.display === "none") {

`              `x.style.display = "block";

`          `} else {

`              `x.style.display = "none";

`          `}

`      `}

`    `</script>

`  `</body>

</html>

gettingstarted@rancher:~$

**Окончание**

Поздравляем! Вы успешно развернули workload - рабочую нагрузку, доступную через NodePort.

**Что дальше?**

Когда вы закончите использовать свою песочницу, уничтожьте сервер Rancher и ваш кластер. См. одно из следующего:

- [Amazon AWS: уничтожение](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/amazon-aws-qs/#destroying-the-environment") ресурса
- [DigitalOcean: уничтожение](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/digital-ocean-qs/#destroying-the-environment") ресурса
- [Vagrant: уничтожение](https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/ "https://github.com/rancher/docs/blob/master/content/rancher/v2.6/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/%7B%7B%3Cbaseurl%3E%7D%7D/rancher/v2.6/en/quick-start-guide/deployment/quickstart-vagrant/#destroying-the-environment") ресурса

