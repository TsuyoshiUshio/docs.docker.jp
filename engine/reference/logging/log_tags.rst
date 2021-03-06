.. -*- coding: utf-8 -*-
.. https://docs.docker.com/engine/reference/logging/log_tags/
.. doc version: 1.9
.. check date: 2015/12/28
.. -----------------------------------------------------------------------------

.. Log Tags

=======================================
ログ用のタグ
=======================================

.. The tag log option specifies how to format a tag that identifies the container’s log messages. By default, the system uses the first 12 characters of the container id. To override this behavior, specify a tag option:

``tag`` ログ・オプションは、コンテナのログ・メッセージを識別するため、どのような形式のタグを使うか指定します。デフォルトでは、システムはコンテナ ID の冒頭12文字を使います。この動作を上書きするには、 ``tag`` オプションを使います。

.. code-block:: bash

   docker run --log-driver=fluentd --log-opt fluentd-address=myhost.local:24224 --log-opt tag="mailer"

.. Docker supports some special template markup you can use when specifying a tag’s value:

Docker はタグの値を指定するための特別なテンプレート・マークアップをサポートしています。

.. Markup 	Description
.. {{.ID}} 	The first 12 characters of the container id.
.. {{.FullID}} 	The full container id.
.. {{.Name}} 	The container name.
.. {{.ImageID}} 	The first 12 characters of the container’s image id.
.. {{.ImageFullID}} 	The container’s full image identifier.
.. {{.ImageName}} 	The name of the image used by the container.

.. list-table::
   :header-rows: 1
   
   * - マークアップ
     - 説明
   * - ``{{.ID}}``
     - コンテナ ID の冒頭 12 文字
   * - ``{{.FullID}}``
     - コンテナの完全 ID
   * - ``{{.Name}}``
     - コンテナ名
   * - ``{{.ImageID}}``
     - イメージ ID の冒頭 12 文字
   * - ``{{.ImageFullId}}``
     - コンテナの完全 ID
   * - ``{{.ImageName}}``
     - コンテナが使っているイメージ名

.. For example, specifying a --log-opt tag="{{.ImageName}}/{{.Name}}/{{.ID}}" value yields syslog log lines like:

例えば、 ``--log-opt tag="{{.ImageName}}/{{.Name}}/{{.ID}}"`` 値を指定すると、 ``syslog`` のログ行は次のようになります。

.. code-block:: bash

   Aug  7 18:33:19 HOSTNAME docker/hello-world/foobar/5790672ab6a0[9103]: Hello from Docker.

.. At startup time, the system sets the container_name field and {{.Name}} in the tags. If you use docker rename to rename a container, the new name is not reflected in the log messages. Instead, these messages continue to use the original container name.

起動時に、システムは ``container_name`` フィールドと ``{{.Name}}`` をタグに設定します。 ``docker rename`` でコンテナ名を変更しても、ログメッセージに新しいコンテナ名は反映されません。そのかわり、これらのメッセージは元々のコンテナ名を使って保存され続けます。

.. For advanced usage, the generated tag’s use go templates and the container’s logging context.

高度な使い方は、 `go テンプレート <http://golang.org/pkg/text/template/>`_ のタグ生成や、コンテナの `ログ内容 <https://github.com/docker/docker/blob/master/daemon/logger/context.go>`_ をご覧ください。

..    Note:The driver specific log options syslog-tag, fluentd-tag and gelf-tag still work for backwards compatibility. However, going forward you should standardize on using the generic tag log option instead.

.. note::

   ドライバがログのオプション ``syslog-tag`` 、 ``fluentd-tag`` 、 ``gelf-tag`` を指定しても後方互換性があります。ですが、これらの代わりに、標準化のため一般的な ``tag`` ログ・オプションを使うべきです。

