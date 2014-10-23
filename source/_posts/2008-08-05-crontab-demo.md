---
title: crontab demo
author: gxbsst
layout: post
permalink: /archives/162
post_views_count:
  - 131
views:
  - 59
categories:
  - 技术感想
---
<pre lang="c">3 # Core Website/ERP &#038; RSS Sync Tools
 4 # m h  dom mon dow   command
 5   0  0   15  *   *    cd /dir &#038;&#038; rake db:ipdb:create
 6   0  0   *   *   *    cd /dir &#038;&#038; RAILS_ENV=production rake report:website_ax_variance >/dev/null 
 7   0  0   *   *   *    cd /dir &#038;&#038; RAILS_ENV=production rake report:website_ax_inventories_variance >/dev/null 
 8 */15 *   *   *   *    cd /dir &#038;&#038; RAILS_ENV=production rake rss:refresh >/dev/null 
 9   0 */4  *   *   *    cd /dir &#038;&#038; RAILS_ENV=production rake ax:hourly >/dev/null 2>&#038;1
10   0 */1  *   *   *    /dir/script/erp_process_batch production >/dev/null 2>&#038;1 &lt;/dev/null
11 # Run the AX Customer/Sales Order Update Every 5 Minutes...
12  */5 *   *   *   *    cd /dir &#038;&#038; RAILS_ENV=production rake erp:sync >/dev/null 
13 
14 # Delete Expired Cache Files
15 */30 *   *   *   *    find /dir/public/downloads/ -noleaf -cmin +30 -delete
16   1  *   *   *   *    find /dir/tmp/sessions -noleaf -name 'ruby_sess*' -ctime +1 -delete
17   1  *   *   *   *    find /dir/tmp/cache/ -noleaf -name “_*.cache” | xargs rm -f
18 */15 *   *   *   *    rm -f /dir/public/{zh_CN.html,cs_CZ.html,es_ES.html,ja_JP.html,index.html}
19   1  *   *   *   *    find /tmp -noleaf -name 'ruby_sess*' -ctime +1 -delete >/dev/null
20 
21 # Backup Databases
22   2  *   *   *   *    /var/www/store/current/script/backup_db.sh 
23   5  0   *   *   0    /var/www/store/current/script/backup_db_weekly.sh
24   00 23  *   *   0    /mail_backup/mailbackup
25 
26 # Security Checks and System Maintance
27 #*/60 *   *   *   *    /bin/df -h
28 # 5  *   *   *   *    /usr/sbin/st_snapshot.hourly # SysTraq
29   1  1   *   *   *    /usr/bin/updatedb
30   00 */8 *   *   *    /usr/bin/chkrootk
31   45 */8 *   *   *    /usr/bin/rkhunt
32   00 5   *   *   *    /usr/local/etc/logcheck.sh


24* #!/bin/bash
EXTENSION=`/bin/date “+%Y-%m-%d”`
/usr/bin/mysqldump -A --default-character-set=utf8 -u root -p passwd database | gzip --fast > /mail_backup/database.$EXTENSION.gz
</pre>

转载请注明：[韦旭红的点点滴滴][1] &raquo; [crontab demo][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/162