.. -*- coding: utf-8 -*-
.. https://docs.docker.com/compose/reference/up/
.. doc version: 1.9
.. check date: 2016/01/19
.. -----------------------------------------------------------------------------

.. up

.. _compse-up:

=======================================
up
=======================================

.. code-block:: bash

   Usage: up [options] [SERVICE...]
   
   Options:
   -d                     Detached mode: Run containers in the background,
                          print new container names.
   --no-color             Produce monochrome output.
   --no-deps              Don't start linked services.
   --force-recreate       Recreate containers even if their configuration and
                          image haven't changed. Incompatible with --no-recreate.
   --no-recreate          If containers already exist, don't recreate them.
                          Incompatible with --force-recreate.
   --no-build             Don't build an image, even if it's missing
   -t, --timeout TIMEOUT  Use this timeout in seconds for container shutdown
                          when attached or when containers are already
                          running. (default: 10)

.. Builds, (re)creates, starts, and attaches to containers for a service.

サービス用のコンテナの構築、作成、起動、アタッチを行います。

.. Unless they are already running, this command also starts any linked services.

既に実行している場合は、このコマンドによってリンクされているサービスも起動します。

.. The docker-compose up command aggregates the output of each container. When the command exits, all containers are stopped. Running docker-compose up -d starts the containers in the background and leaves them running.

``docker-compose up`` コマンドは各コンテナの出力を統合します。コマンドを終了（exit）すると、全てのコンテナを停止します。 ``docker-compose up -d`` で実行すると、コンテナをバックグラウンドで起動し、実行し続けます。

.. If there are existing containers for a service, and the service’s configuration or image was changed after the container’s creation, docker-compose up picks up the changes by stopping and recreating the containers (preserving mounted volumes). To prevent Compose from picking up changes, use the --no-recreate flag.

もしサービス用のコンテナが存在している場合、かつ、コンテナを作成後にサービスの設定やイメージを変更している場合は、 ``docker-compose up -d``を実行スト、 設定を反映するためにコンテナを停止・再作成します（マウントしているボリュームは、そのまま保持します）。Compose が設定を反映させないようにするには、 ``--no-cecreate`` フラグを使います。

.. If you want to force Compose to stop and recreate all containers, use the --force-recreate flag.

もしも Compose で処理時、強制的に全てのコンテナを停止・再作成するには ``--force-recreate`` フラグを使います。