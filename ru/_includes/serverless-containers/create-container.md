{% list tabs group=instructions %}

- Консоль управления {#console}

  1. В [консоли управления]({{ link-console-main }}) перейдите в [каталог](../../resource-manager/concepts/resources-hierarchy.md#folder), в котором хотите создать [контейнер](../../serverless-containers/concepts/container.md).
  1. Выберите сервис **{{ ui-key.yacloud.iam.folder.dashboard.label_serverless-containers }}**.
  1. Нажмите кнопку **{{ ui-key.yacloud.serverless-containers.button_create-container }}**.
  1. Введите имя и описание контейнера. Формат имени:

     {% include [name-format](../../_includes/name-format.md) %}

  1. Нажмите кнопку **{{ ui-key.yacloud.common.create }}**.

- CLI {#cli}

  {% include [cli-install](../cli-install.md) %}

  {% include [default-catalogue](../default-catalogue.md) %}

  Чтобы создать [контейнер](../../serverless-containers/concepts/container.md), выполните команду:

  ```bash
  yc serverless container create --name <имя_контейнера>
  ```

  Результат:

  ```text
  id: bba3fva6ka5g********
  folder_id: b1gqvft7kjk3********
  created_at: "2021-07-09T14:49:00.891Z"
  name: my-beta-container
  url: https://bba3fva6ka5g********.{{ serverless-containers-host }}/
  status: ACTIVE
  ```

- {{ TF }} {#tf}

  {% include [terraform-definition](../../_tutorials/_tutorials_includes/terraform-definition.md) %}

  {% include [terraform-install](../../_includes/terraform-install.md) %}

  Чтобы создать [контейнер](../../serverless-containers/concepts/container.md) и его [ревизию](../../serverless-containers/operations/manage-revision.md):

  {% note info %}

  {% include [revision-service-account-note](revision-service-account-note.md) %}

  {% endnote %}

  1. Опишите в конфигурационном файле параметры ресурсов, которые необходимо создать:
     * `name` — имя контейнера. Обязательный параметр. Требования к имени:

       {% include [name-format](../../_includes/name-format.md) %}

     * `memory` — объем памяти в МБ, выделенный контейнеру. По умолчанию — 128 МБ.
     * `service_account_id` — идентификатор [сервисного аккаунта](../../iam/concepts/users/service-accounts.md).
     * `url` — URL [Docker-образа](../../container-registry/concepts/docker-image.md) в [{{ container-registry-full-name }}](../../container-registry/).

     >Пример структуры конфигурационного файла:
     >
     >```hcl
     >provider "yandex" {
     >  token     = "<OAuth>"
     >  cloud_id  = "<идентификатор_облака>"
     >  folder_id = "<идентификатор_каталога>"
     >  zone      = "{{ region-id }}-a"
     >}
     >
     >resource "yandex_serverless_container" "test-container" {
     >   name               = "<имя_контейнера>"
     >   memory             = <объем_памяти>
     >   service_account_id = "<идентификатор_сервисного_аккаунта>"
     >   image {
     >       url = "<URL_Docker-образа>"
     >   }
     >}
     >```

     Более подробную информацию о параметрах ресурса `yandex_serverless_container` в {{ TF }}, см. в [документации провайдера]({{ tf-provider-resources-link }}/serverless_container).
  1. Проверьте корректность конфигурационных файлов.
     1. В командной строке перейдите в папку, где вы создали конфигурационный файл.
     1. Выполните проверку с помощью команды:

        ```bash
        terraform plan
        ```

     Если конфигурация описана верно, в терминале отобразится список создаваемых ресурсов и их параметров. Если в конфигурации есть ошибки, {{ TF }} на них укажет.
  1. Разверните облачные ресурсы.
     1. Если в конфигурации нет ошибок, выполните команду:

        ```bash
        terraform apply
        ```

     1. Подтвердите создание ресурсов: введите в терминал слово `yes` и нажмите **Enter**.

        После этого в указанном [каталоге](../../resource-manager/concepts/resources-hierarchy.md#folder) будут созданы все требуемые ресурсы. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-main }}) или с помощью команды [CLI](../../cli/):

        ```bash
        yc serverless container list 
        ```

- API {#api}

  Чтобы создать [контейнер](../../serverless-containers/concepts/container.md), воспользуйтесь методом REST API [create](../../serverless-containers/containers/api-ref/Container/create.md) для ресурса [Container](../../serverless-containers/containers/api-ref/Container/index.md) или вызовом gRPC API [ContainerService/Create](../../serverless-containers/containers/api-ref/grpc/container_service.md#Create).

{% endlist %}