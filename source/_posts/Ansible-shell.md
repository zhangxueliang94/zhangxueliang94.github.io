---
title: Ansible 
date: 2018-11-22 
tags: [shell]
categories: 技术
---

###  case ansible

``` case shell
#! /bin/sh                  
#2018-10-12
menu(){
echo -e "---------10 update batch --------\n--------21 update config1 ----------\n-------- 22 update config2 -------\n---------31 update console1 ---------\n-------- 32 update console2--------\n----------41 update cwx1 --------\n-------42 update cwx2 --------\n--------51 update gateway1-------\n--------52 update gateway2 -------\n--------61 update global1-------\n-------- 62 update global2--------\n--------71 update internet1--------\n--------72 update internet2 --------\n---------80 update manage--------\n--------91 update registry1--------\n--------92 update registry2 --------\n--------101 update web1--------\n--------102 update web2--------\n--------110 tob update index.html--------\n--------120 admin update index.html--------\n---------131 update message1--------\n--------132 update message2--------\n--------0 quit program--------"
}
source /etc/profile
menu
cmd="ansible-playbook"
dir="/data/doploy"
read -p "please input update package num:" a
while [ $a -ne 0 ]
do
case $a in
10)
 $cmd $dir/batch/batch.yml
;;
21)
 $cmd $dir/config/config1.yml
;;
22)
 $cmd $dir/config/config2.yml
;;
31)  
 $cmd $dir/console/console1.yml
;;
32)  
 $cmd $dir/console/console2.yml
;;
41) 
 $cmd $dir/cwx/cwx1.yml
;; 
42) 
 $cmd $dir/cwx/cwx2.yml
;; 
51)
 $cmd $dir/gateway/gateway1.yml
;;  
52)
 $cmd $dir/gateway/gateway2.yml
;;  
61)
 $cmd $dir/global/global1.yml
;;  
62)
 $cmd $dir/global/global2.yml
;;  
71)
 $cmd $dir/internet/internet1.yml  
;;
72)
 $cmd $dir/internet/internet2.yml  
;;
80)
 $cmd $dir/manage/manage.yml
;;  
91)
 $cmd $dir/registry/registry1.yml 
;; 
92)
 $cmd $dir/registry/registry2.yml 
;; 
101)
 $cmd $dir/web/web1.yml
;;
102)
 $cmd $dir/web/web2.yml
;;
110)
$cmd $dir/html-formal/html-formal.yml
;;
120)
$cmd $dir/yxqn-admin/yxqn-admin.yml
;;
131)
$cmd $dir/message/message1.yml 
;;
132)
$cmd $dir/message/message2.yml     
;;
*)
  echo "input error ,please input again"
  menu
;;
esac
   read -p "please input update package num:" a
done

```

### ansible-playbook

```
- hosts: cwx1
  user: root
  vars:
  - var1: "rename.sh"
  - var2: "yxqn-cwx-1.0-SNAPSHOT.jar"
  - var3: "cwx"
  
  tasks:
  - name: stop {{ var3 }}  service
    shell: /bin/sh -x   /data/yxqn/{{ var3 }}/stop.sh
  
  - name: move rename file
    script: /data/doploy/{{ var3 }}/{{ var1 }} 

  - name: copy {{ var3 }} file
    copy: src=/home/formal/{{ var2 }} dest=/data/yxqn/{{ var3 }}

  - name: start {{ var3 }} service
    shell: /bin/sh -x  /data/yxqn/{{ var3 }}/{{ var3 }}.sh 

```

### rename.sh 
```
#! /bin/sh
microservice(){
caldate=`date +%Y%m%d`
name="cwx"
file="yxqn-$name-1.0-SNAPSHOT.jar"
dir="/data/yxqn/$name"
cd $dir
mv $file $file\.$caldate
ls bak || mkdir bak
mv $file\.$caldate bak
}
 microservice


```



