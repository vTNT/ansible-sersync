# Ansible Role: sersync

install sersync

## info
sersync主要用于服务器同步，web镜像等功能。基于boost1.43.0,inotify api,rsync command.开发。由金山公司开发并开源的同步软件。sersync部署在源服务器上，在目标服务器上部署好普通的rsync服务后，在源服务器上启动sersync即可，sersync通过解析xml配置文件来获取相关rsync时的一些策略。

address： https://code.google.com/archive/p/sersync/


## 要求

only run on Ubuntu。

## os env

ansible `2.x`
os `Ubuntu 14.04`

## var
    sersync_xfs: "false"
    sersync_exclude: []
    sersync_watch: "/tmp"

    sersync_path: "/usr/local/sersync"
    sersync_rsync: {} # {"port":873, "name":data1, "user":t1, "pass":123456,"params":"-artuz"}
    sersync_host_list: ["127.0.0.1"]
    sersync_rsync_passwordfile: "/etc/rsync.pass"

    sersync_rsync_start: "false"
    sersync_rsync_timeout: "100"
    sersync_rsync_ssh: "false"

    sersync_inotify_delete: true
    sersync_inotify_createFolder: true
    sersync_inotify_createFile: false
    sersync_inotify_closeWrite: true
    sersync_inotify_moveFrom: true
    sersync_inotify_moveTo: true
    sersync_inotify_attrib: false
    sersync_inotify_modify: false

    sersync_failLog: "/tmp/rsync_fail_log.sh"
    sersync_crontab: "false"
    sersync_schedule: "600"

## require

rsync

## Example Playbook

	install sersync：
    ---
    - name: Test the plabybook API.
    hosts: all
    remote_user: root
    gather_facts: no
    roles:
      - role: ansible-sersync
        sersync_inotify_createFolder: false
        sersync_watch: "/data/LOneClient/data"
        sersync_host_list: ["172.17.0.3", "172.17.0.5"]
        sersync_rsync: {"name":stock, "user":nobody, "pass":123456789}
        sersync_rsync_passwordfile: "/etc/password.rsync"

