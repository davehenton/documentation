---
title: Using RethinkDB In CI/CD with Codeship Basic
shortTitle: RethinkDB
tags:
  - services
  - databases
  - rethinkdb
  - db
menus:
  basic/db:
    title: RethinkDB
    weight: 6
redirect_from:
  - /databases/rethinkdb/
  - /classic/getting-started/rethinkdb/
categories:
  - Databases
---

* include a table of contents
{:toc}

RethinkDB is installed on our test VMs but not running by default. To use the RethinkDB during your builds, start the service via the following command:

```shell
sudo /etc/init.d/rethinkdb start
```

RethinkDB runs on the default port. Administrative HTTP connections are available via port `50836`.
