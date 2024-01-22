1. SELinux - когда все запрещено
2. Запустить nginx на нестандартном порту 3-мя разными способами:
     переключатели setsebool - результат typescript_setsebool;
     добавление нестандартного порта в имеющийся тип - результат typescript_semanage;
     формирование и установка модуля SELinux - результат typescript_semodule.
3. Обеспечить работоспособность приложения при включенном selinux - заходим vagrant ssh ns01; sudo -i; cat /var/log/audit/audit.log | audit2why - в логах мы видим, что ошибка в контексте безопасности, используется тип etc_t, когда необходим named_t, выполняем chcon -R -t named_zone_t /etc/named; setsebool -P named_write_master_zones 1. Заходим в vagrant ssh client, все работает. Результат typescript_selinux_dns_problems.
