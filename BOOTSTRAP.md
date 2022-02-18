# Bootstrapping

## Start archlinux from an USB key.
See https://wiki.archlinux.org/title/Iwd#iwctl for details
`timedatectl set-ntp true`
`passwd`
`systemctl start sshd`
Find you IP using `ip address`

## Creating partitions
Use `gdisk` to create a partition table:

Number | Start | End | Code | Name
1 | 2048 | 4096 | 1.0MiB | EF02 | BIOS boot partition
2 | 4096 | 1130495 | 550MiB | EF00 | BIOS boot partition
3 | 1130496 | * | Rest | 8309 | Linux LUKS

Edit inventory and set up you machine under bootstrap

`cryptsetup luksFormat /dev/nvme0n1p3`
`cryptsetup open --perf-no_read_workqueue --perf-no_write_workqueue --persistent /dev/nvme0n1p3 cryptroot`
`ansible-playbook bootstrap.yml -uroot`
