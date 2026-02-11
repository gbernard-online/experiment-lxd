```
sudo snap set lxd criu.enable=true
...
before install

$ lxc config show
config:
  cluster.https_address: ubuntu-1.qemu.lan:8443
  core.https_address: '[::]:8443'

lxc cluster update-certificate server-qemu-2026.crt server-qemu.pem
```

```bash
$ hostname 
ubuntu-1

$ sudo snap install lxd
2026-02-11T10:18:13Z INFO Waiting for automatic snapd restart...
lxd (5.21/stable) 5.21.4-de343be from Canonical✓ installed

$ sudo lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: yes
What IP address or DNS name should be used to reach this server? [default=172.16.0.209]: ubuntu-1.qemu.lan
Are you joining an existing cluster? (yes/no) [default=no]:
What member name should be used to identify this server in the cluster? [default=ubuntu-1]:
Do you want to configure a new local storage pool? (yes/no) [default=yes]:
Name of the storage backend to use (btrfs, dir, lvm, zfs) [default=zfs]: dir
Do you want to configure a new remote storage pool? (yes/no) [default=no]:
Would you like to connect to a MAAS server? (yes/no) [default=no]:
Would you like to configure LXD to use an existing bridge or host interface? (yes/no) [default=no]:
Would you like to create a new Fan overlay network? (yes/no) [default=yes]:
What subnet should be used as the Fan underlay? [default=auto]:
Would you like stale cached images to be updated automatically? (yes/no) [default=yes]:
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: yes
config:
  core.https_address: ubuntu-1.qemu.lan:8443
networks:
- config:
    bridge.mode: fan
    fan.underlay_subnet: auto
  description: ""
  name: lxdfan0
  type: ""
  project: default
storage_pools:
- config: {}
  description: ""
  name: local
  driver: dir
storage_volumes: []
profiles:
- config: {}
  description: ""
  devices:
    eth0:
      name: eth0
      network: lxdfan0
      type: nic
    root:
      path: /
      pool: local
      type: disk
  name: default
projects: []
cluster:
  server_name: ubuntu-1
  enabled: true
  member_config: []
  cluster_address: ""
  cluster_certificate: ""
  server_address: ""
  cluster_password: ""
  cluster_token: ""
  cluster_certificate_path: ""

$ sudo lxd cluster show
# Latest dqlite segment ID: 28

members:
- id: 1
  name: ubuntu-1
  address: ubuntu-1.qemu.lan:8443
  role: voter

$ lxc info
To start your first container, try: lxc launch ubuntu:24.04
Or for a virtual machine: lxc launch ubuntu:24.04 --vm

config:
  cluster.https_address: ubuntu-1.qemu.lan:8443
  core.https_address: ubuntu-1.qemu.lan:8443
api_extensions:
- storage_zfs_remove_snapshots
- container_host_shutdown_timeout
- container_stop_priority
- container_syscall_filtering
- auth_pki
- container_last_used_at
- etag
- patch
- usb_devices
- https_allowed_credentials
- image_compression_algorithm
- directory_manipulation
- container_cpu_time
- storage_zfs_use_refquota
- storage_lvm_mount_options
- network
- profile_usedby
- container_push
- container_exec_recording
- certificate_update
- container_exec_signal_handling
- gpu_devices
- container_image_properties
- migration_progress
- id_map
- network_firewall_filtering
- network_routes
- storage
- file_delete
- file_append
- network_dhcp_expiry
- storage_lvm_vg_rename
- storage_lvm_thinpool_rename
- network_vlan
- image_create_aliases
- container_stateless_copy
- container_only_migration
- storage_zfs_clone_copy
- unix_device_rename
- storage_lvm_use_thinpool
- storage_rsync_bwlimit
- network_vxlan_interface
- storage_btrfs_mount_options
- entity_description
- image_force_refresh
- storage_lvm_lv_resizing
- id_map_base
- file_symlinks
- container_push_target
- network_vlan_physical
- storage_images_delete
- container_edit_metadata
- container_snapshot_stateful_migration
- storage_driver_ceph
- storage_ceph_user_name
- resource_limits
- storage_volatile_initial_source
- storage_ceph_force_osd_reuse
- storage_block_filesystem_btrfs
- resources
- kernel_limits
- storage_api_volume_rename
- network_sriov
- console
- restrict_devlxd
- migration_pre_copy
- infiniband
- maas_network
- devlxd_events
- proxy
- network_dhcp_gateway
- file_get_symlink
- network_leases
- unix_device_hotplug
- storage_api_local_volume_handling
- operation_description
- clustering
- event_lifecycle
- storage_api_remote_volume_handling
- nvidia_runtime
- container_mount_propagation
- container_backup
- devlxd_images
- container_local_cross_pool_handling
- proxy_unix
- proxy_udp
- clustering_join
- proxy_tcp_udp_multi_port_handling
- network_state
- proxy_unix_dac_properties
- container_protection_delete
- unix_priv_drop
- pprof_http
- proxy_haproxy_protocol
- network_hwaddr
- proxy_nat
- network_nat_order
- container_full
- backup_compression
- nvidia_runtime_config
- storage_api_volume_snapshots
- storage_unmapped
- projects
- network_vxlan_ttl
- container_incremental_copy
- usb_optional_vendorid
- snapshot_scheduling
- snapshot_schedule_aliases
- container_copy_project
- clustering_server_address
- clustering_image_replication
- container_protection_shift
- snapshot_expiry
- container_backup_override_pool
- snapshot_expiry_creation
- network_leases_location
- resources_cpu_socket
- resources_gpu
- resources_numa
- kernel_features
- id_map_current
- event_location
- storage_api_remote_volume_snapshots
- network_nat_address
- container_nic_routes
- cluster_internal_copy
- seccomp_notify
- lxc_features
- container_nic_ipvlan
- network_vlan_sriov
- storage_cephfs
- container_nic_ipfilter
- resources_v2
- container_exec_user_group_cwd
- container_syscall_intercept
- container_disk_shift
- storage_shifted
- resources_infiniband
- daemon_storage
- instances
- image_types
- resources_disk_sata
- clustering_roles
- images_expiry
- resources_network_firmware
- backup_compression_algorithm
- ceph_data_pool_name
- container_syscall_intercept_mount
- compression_squashfs
- container_raw_mount
- container_nic_routed
- container_syscall_intercept_mount_fuse
- container_disk_ceph
- virtual-machines
- image_profiles
- clustering_architecture
- resources_disk_id
- storage_lvm_stripes
- vm_boot_priority
- unix_hotplug_devices
- api_filtering
- instance_nic_network
- clustering_sizing
- firewall_driver
- projects_limits
- container_syscall_intercept_hugetlbfs
- limits_hugepages
- container_nic_routed_gateway
- projects_restrictions
- custom_volume_snapshot_expiry
- volume_snapshot_scheduling
- trust_ca_certificates
- snapshot_disk_usage
- clustering_edit_roles
- container_nic_routed_host_address
- container_nic_ipvlan_gateway
- resources_usb_pci
- resources_cpu_threads_numa
- resources_cpu_core_die
- api_os
- container_nic_routed_host_table
- container_nic_ipvlan_host_table
- container_nic_ipvlan_mode
- resources_system
- images_push_relay
- network_dns_search
- container_nic_routed_limits
- instance_nic_bridged_vlan
- network_state_bond_bridge
- usedby_consistency
- custom_block_volumes
- clustering_failure_domains
- resources_gpu_mdev
- console_vga_type
- projects_limits_disk
- network_type_macvlan
- network_type_sriov
- container_syscall_intercept_bpf_devices
- network_type_ovn
- projects_networks
- projects_networks_restricted_uplinks
- custom_volume_backup
- backup_override_name
- storage_rsync_compression
- network_type_physical
- network_ovn_external_subnets
- network_ovn_nat
- network_ovn_external_routes_remove
- tpm_device_type
- storage_zfs_clone_copy_rebase
- gpu_mdev
- resources_pci_iommu
- resources_network_usb
- resources_disk_address
- network_physical_ovn_ingress_mode
- network_ovn_dhcp
- network_physical_routes_anycast
- projects_limits_instances
- network_state_vlan
- instance_nic_bridged_port_isolation
- instance_bulk_state_change
- network_gvrp
- instance_pool_move
- gpu_sriov
- pci_device_type
- storage_volume_state
- network_acl
- migration_stateful
- disk_state_quota
- storage_ceph_features
- projects_compression
- projects_images_remote_cache_expiry
- certificate_project
- network_ovn_acl
- projects_images_auto_update
- projects_restricted_cluster_target
- images_default_architecture
- network_ovn_acl_defaults
- gpu_mig
- project_usage
- network_bridge_acl
- warnings
- projects_restricted_backups_and_snapshots
- clustering_join_token
- clustering_description
- server_trusted_proxy
- clustering_update_cert
- storage_api_project
- server_instance_driver_operational
- server_supported_storage_drivers
- event_lifecycle_requestor_address
- resources_gpu_usb
- clustering_evacuation
- network_ovn_nat_address
- network_bgp
- network_forward
- custom_volume_refresh
- network_counters_errors_dropped
- metrics
- image_source_project
- clustering_config
- network_peer
- linux_sysctl
- network_dns
- ovn_nic_acceleration
- certificate_self_renewal
- instance_project_move
- storage_volume_project_move
- cloud_init
- network_dns_nat
- database_leader
- instance_all_projects
- clustering_groups
- ceph_rbd_du
- instance_get_full
- qemu_metrics
- gpu_mig_uuid
- event_project
- clustering_evacuation_live
- instance_allow_inconsistent_copy
- network_state_ovn
- storage_volume_api_filtering
- image_restrictions
- storage_zfs_export
- network_dns_records
- storage_zfs_reserve_space
- network_acl_log
- storage_zfs_blocksize
- metrics_cpu_seconds
- instance_snapshot_never
- certificate_token
- instance_nic_routed_neighbor_probe
- event_hub
- agent_nic_config
- projects_restricted_intercept
- metrics_authentication
- images_target_project
- cluster_migration_inconsistent_copy
- cluster_ovn_chassis
- container_syscall_intercept_sched_setscheduler
- storage_lvm_thinpool_metadata_size
- storage_volume_state_total
- instance_file_head
- instances_nic_host_name
- image_copy_profile
- container_syscall_intercept_sysinfo
- clustering_evacuation_mode
- resources_pci_vpd
- qemu_raw_conf
- storage_cephfs_fscache
- network_load_balancer
- vsock_api
- instance_ready_state
- network_bgp_holdtime
- storage_volumes_all_projects
- metrics_memory_oom_total
- storage_buckets
- storage_buckets_create_credentials
- metrics_cpu_effective_total
- projects_networks_restricted_access
- storage_buckets_local
- loki
- acme
- internal_metrics
- cluster_join_token_expiry
- remote_token_expiry
- init_preseed
- storage_volumes_created_at
- cpu_hotplug
- projects_networks_zones
- network_txqueuelen
- cluster_member_state
- instances_placement_scriptlet
- storage_pool_source_wipe
- zfs_block_mode
- instance_generation_id
- disk_io_cache
- amd_sev
- storage_pool_loop_resize
- migration_vm_live
- ovn_nic_nesting
- oidc
- network_ovn_l3only
- ovn_nic_acceleration_vdpa
- cluster_healing
- instances_state_total
- auth_user
- security_csm
- instances_rebuild
- numa_cpu_placement
- custom_volume_iso
- network_allocations
- storage_api_remote_volume_snapshot_copy
- zfs_delegate
- operations_get_query_all_projects
- metadata_configuration
- syslog_socket
- event_lifecycle_name_and_project
- instances_nic_limits_priority
- disk_initial_volume_configuration
- operation_wait
- cluster_internal_custom_volume_copy
- disk_io_bus
- storage_cephfs_create_missing
- instance_move_config
- ovn_ssl_config
- init_preseed_storage_volumes
- metrics_instances_count
- server_instance_type_info
- resources_disk_mounted
- server_version_lts
- oidc_groups_claim
- loki_config_instance
- storage_volatile_uuid
- import_instance_devices
- instances_uefi_vars
- instances_migration_stateful
- container_syscall_filtering_allow_deny_syntax
- access_management
- vm_disk_io_limits
- storage_volumes_all
- instances_files_modify_permissions
- image_restriction_nesting
- container_syscall_intercept_finit_module
- device_usb_serial
- network_allocate_external_ips
- explicit_trust_token
- instance_import_conversion
- instance_create_start
- devlxd_images_vm
- instance_protection_start
- disk_io_bus_virtio_blk
- metadata_configuration_entity_types
- network_allocations_ovn_uplink
- network_ovn_uplink_vlan
- shared_custom_block_volumes
- metrics_api_requests
- projects_limits_disk_pool
- access_management_tls
- state_logical_cpus
- vm_limits_cpu_pin_strategy
- gpu_cdi
- metadata_configuration_scope
- unix_device_hotplug_ownership_inherit
- unix_device_hotplug_subsystem_device_option
- storage_ceph_osd_pool_size
- network_get_target
- network_zones_all_projects
- vm_root_volume_attachment
- projects_limits_uplink_ips
- entities_with_entitlements
- profiles_all_projects
- storage_driver_powerflex
- storage_driver_pure
- cloud_init_ssh_keys
- oidc_scopes
- project_default_network_and_storage
- ubuntu_pro_guest_attach
- images_all_projects
- client_cert_presence
- resources_device_fs_uuid
- clustering_groups_used_by
- container_bpf_delegation
- override_snapshot_profiles_on_copy
- backup_metadata_version
- storage_buckets_all_projects
- network_acls_all_projects
- networks_all_projects
- clustering_restore_skip_mode
- disk_io_threads_virtiofsd
- oidc_client_secret
- pci_hotplug
- device_patch_removal
api_status: stable
api_version: "1.0"
auth: trusted
public: false
auth_methods:
- tls
client_certificate: false
auth_user_name: user
auth_user_method: unix
environment:
  addresses:
  - ubuntu-1.qemu.lan:8443
  architectures:
  - x86_64
  - i686
  backup_metadata_version_range:
  - 1
  - 2
  certificate: |
    -----BEGIN CERTIFICATE-----
    MIIB6zCCAXCgAwIBAgIRAOt7X7eWVMvReGjd1dNJSN4wCgYIKoZIzj0EAwMwJjEM
    MAoGA1UEChMDTFhEMRYwFAYDVQQDDA1yb290QHVidW50dS0xMB4XDTI2MDIxMTEw
    MjAzMVoXDTM2MDIwOTEwMjAzMVowJjEMMAoGA1UEChMDTFhEMRYwFAYDVQQDDA1y
    b290QHVidW50dS0xMHYwEAYHKoZIzj0CAQYFK4EEACIDYgAE+rKZCP7zL8cjNIG6
    cQ+n8X5KCl4IVGqD0PcKXW8NZuDVqKxHr0ynlW1e2/fUq9ELhClOSdNtDCqqsgh7
    8XBJnvVjRon4E+u3zzuWRMo9GBHX8v5a0AOUgB1TMv2w8iW4o2IwYDAOBgNVHQ8B
    Af8EBAMCBaAwEwYDVR0lBAwwCgYIKwYBBQUHAwEwDAYDVR0TAQH/BAIwADArBgNV
    HREEJDAiggh1YnVudHUtMYcEfwAAAYcQAAAAAAAAAAAAAAAAAAAAATAKBggqhkjO
    PQQDAwNpADBmAjEA+/mDQCjVvlgaGyWvB5t6pJBfR+RvwkRk/7P6lb6qm7x203xW
    m+/pc+2DzLZY6HJfAjEA/LWFYYQ5/XTQN0Vv7B2wQkVjOhcGewC8uTX2S58USLxp
    eNePpqw4W8YlwgEDdkQ+
    -----END CERTIFICATE-----
  certificate_fingerprint: d8167c9d5226c4dfed501a47f557eab08aac3c5ac71daa5ee4024ed87db2b238
  driver: lxc | qemu
  driver_version: 6.0.4 | 8.2.2
  instance_types:
  - container
  - virtual-machine
  firewall: nftables
  kernel: Linux
  kernel_architecture: x86_64
  kernel_features:
    bpf_token: "false"
    idmapped_mounts: "true"
    netnsid_getifaddrs: "true"
    seccomp_listener: "true"
    seccomp_listener_continue: "true"
    uevent_injection: "true"
    unpriv_binfmt: "true"
    unpriv_fscaps: "true"
  kernel_version: 6.8.0-100-generic
  lxc_features:
    cgroup2: "true"
    core_scheduling: "true"
    devpts_fd: "true"
    idmapped_mounts_v2: "true"
    mount_injection_file: "true"
    network_gateway_device_route: "true"
    network_ipvlan: "true"
    network_l2proxy: "true"
    network_phys_macvlan_mtu: "true"
    network_veth_router: "true"
    pidfd: "true"
    seccomp_allow_deny_syntax: "true"
    seccomp_notify: "true"
    seccomp_proxy_send_notify_fd: "true"
  os_name: Ubuntu
  os_version: "24.04"
  project: default
  server: lxd
  server_clustered: true
  server_event_mode: full-mesh
  server_name: ubuntu-1
  server_pid: 2502
  server_version: 5.21.4
  server_lts: true
  storage: dir
  storage_version: "1"
  storage_supported_drivers:
  - name: pure
    version: 2.1.9 (iscsiadm) / 1.16 (nvme-cli)
    remote: true
  - name: zfs
    version: 2.2.2-0ubuntu9.4
    remote: false
  - name: btrfs
    version: 5.16.2
    remote: false
  - name: ceph
    version: 17.2.9
    remote: true
  - name: cephfs
    version: 17.2.9
    remote: true
  - name: cephobject
    version: 17.2.9
    remote: true
  - name: dir
    version: "1"
    remote: false
  - name: lvm
    version: 2.03.11(2) (2021-01-08) / 1.02.175 (2021-01-08) / 4.48.0
    remote: false
  - name: powerflex
    version: 1.16 (nvme-cli)
    remote: true

$ lxc info | fgrep fingerprint
  certificate_fingerprint: d8167c9d5226c4dfed501a47f557eab08aac3c5ac71daa5ee4024ed87db2b238

$ lxc cluster list
+----------+--------------------------------+-----------------+--------------+----------------+-------------+--------+-------------------+
|   NAME   |              URL               |      ROLES      | ARCHITECTURE | FAILURE DOMAIN | DESCRIPTION | STATE  |      MESSAGE      |
+----------+--------------------------------+-----------------+--------------+----------------+-------------+--------+-------------------+
| ubuntu-1 | https://ubuntu-1.qemu.lan:8443 | database-leader | x86_64       | default        |             | ONLINE | Fully operational |
|          |                                | database        |              |                |             |        |                   |
+----------+--------------------------------+-----------------+--------------+----------------+-------------+--------+-------------------+

$ lxc monitor --pretty
[...]

$ lxc cluster add ubuntu-2.qemu.lan
Member ubuntu-2.qemu.lan join token:
[...]

$ lxc cluster add ubuntu-3.qemu.lan
Member ubuntu-3.qemu.lan join token:
[...]
```

```bash
$ hostname 
ubuntu-2

$ sudo snap install lxd
2026-02-11T10:23:54Z INFO Waiting for automatic snapd restart...
lxd (5.21/stable) 5.21.4-de343be from Canonical✓ installed

$ lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: yes
What IP address or DNS name should be used to reach this server? [default=172.16.0.210]: ubuntu-2.qemu.lan
Are you joining an existing cluster? (yes/no) [default=no]: yes
Error: Joining an existing cluster requires root privileges

$ sudo lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: yes
What IP address or DNS name should be used to reach this server? [default=172.16.0.210]: ubuntu-2.qemu.lan
Are you joining an existing cluster? (yes/no) [default=no]: yes
Do you have a join token? (yes/no/[token]) [default=no]: yes
Please provide join token: eyJzZXJ2ZXJfbmFtZSI6InVidW50dS0yLnFlbXUubGFuIiwiZmluZ2VycHJpbnQiOiJkODE2N2M5ZDUyMjZjNGRmZWQ1MDFhNDdmNTU3ZWFiMDhhYWMzYzVhYzcxZGFhNWVlNDAyNGVkODdkYjJiMjM4IiwiYWRkcmVzc2VzIjpbInVidW50dS0xLnFlbXUubGFuOjg0NDMiXSwic2VjcmV0IjoiMDEwMmM3YzUzYzBhZWJhZjUxNTAxNjcyYmUyYTM4ZmY0YjljZTlmZTE1Y2I4MzYwYjcwNDQyNzdlZDM0NDBlZiIsImV4cGlyZXNfYXQiOiIyMDI2LTAyLTExVDEzOjMzOjQxLjU2MTAzNzkxM1oifQ==
All existing data is lost when joining a cluster, continue? (yes/no) [default=no] yes
Choose "source" property for storage pool "local":
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: yes
config: {}
networks: []
storage_pools: []
storage_volumes: []
profiles: []
projects: []
cluster:
  server_name: ubuntu-2.qemu.lan
  enabled: true
  member_config:
  - entity: storage-pool
    name: local
    key: source
    value: ""
    description: '"source" property for storage pool "local"'
  cluster_address: ubuntu-1.qemu.lan:8443
  cluster_certificate: |
    -----BEGIN CERTIFICATE-----
    MIIB6zCCAXCgAwIBAgIRAOt7X7eWVMvReGjd1dNJSN4wCgYIKoZIzj0EAwMwJjEM
    MAoGA1UEChMDTFhEMRYwFAYDVQQDDA1yb290QHVidW50dS0xMB4XDTI2MDIxMTEw
    MjAzMVoXDTM2MDIwOTEwMjAzMVowJjEMMAoGA1UEChMDTFhEMRYwFAYDVQQDDA1y
    b290QHVidW50dS0xMHYwEAYHKoZIzj0CAQYFK4EEACIDYgAE+rKZCP7zL8cjNIG6
    cQ+n8X5KCl4IVGqD0PcKXW8NZuDVqKxHr0ynlW1e2/fUq9ELhClOSdNtDCqqsgh7
    8XBJnvVjRon4E+u3zzuWRMo9GBHX8v5a0AOUgB1TMv2w8iW4o2IwYDAOBgNVHQ8B
    Af8EBAMCBaAwEwYDVR0lBAwwCgYIKwYBBQUHAwEwDAYDVR0TAQH/BAIwADArBgNV
    HREEJDAiggh1YnVudHUtMYcEfwAAAYcQAAAAAAAAAAAAAAAAAAAAATAKBggqhkjO
    PQQDAwNpADBmAjEA+/mDQCjVvlgaGyWvB5t6pJBfR+RvwkRk/7P6lb6qm7x203xW
    m+/pc+2DzLZY6HJfAjEA/LWFYYQ5/XTQN0Vv7B2wQkVjOhcGewC8uTX2S58USLxp
    eNePpqw4W8YlwgEDdkQ+
    -----END CERTIFICATE-----
  server_address: ubuntu-2.qemu.lan:8443
  cluster_password: ""
  cluster_token: ""
  cluster_certificate_path: ""

$ lxc cluster list
+-------------------+--------------------------------+------------------+--------------+----------------+-------------+--------+-------------------+
|       NAME        |              URL               |      ROLES       | ARCHITECTURE | FAILURE DOMAIN | DESCRIPTION | STATE  |      MESSAGE      |
+-------------------+--------------------------------+------------------+--------------+----------------+-------------+--------+-------------------+
| ubuntu-1          | https://ubuntu-1.qemu.lan:8443 | database-leader  | x86_64       | default        |             | ONLINE | Fully operational |
|                   |                                | database         |              |                |             |        |                   |
+-------------------+--------------------------------+------------------+--------------+----------------+-------------+--------+-------------------+
| ubuntu-2.qemu.lan | https://ubuntu-2.qemu.lan:8443 | database-standby | x86_64       | default        |             | ONLINE | Fully operational |
+-------------------+--------------------------------+------------------+--------------+----------------+-------------+--------+-------------------+
```


```bash
$ hostname 
ubuntu-3

$ sudo snap install lxd
2026-02-11T10:23:54Z INFO Waiting for automatic snapd restart...
lxd (5.21/stable) 5.21.4-de343be from Canonical✓ installed

$ sudo lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: yes
What IP address or DNS name should be used to reach this server? [default=172.16.0.212]: ubuntu-3.qemu.lan
Are you joining an existing cluster? (yes/no) [default=no]: yes
Do you have a join token? (yes/no/[token]) [default=no]: yes
Please provide join token: eyJzZXJ2ZXJfbmFtZSI6InVidW50dS0zIiwiZmluZ2VycHJpbnQiOiJkODE2N2M5ZDUyMjZjNGRmZWQ1MDFhNDdmNTU3ZWFiMDhhYWMzYzVhYzcxZGFhNWVlNDAyNGVkODdkYjJiMjM4IiwiYWRkcmVzc2VzIjpbInVidW50dS0xLnFlbXUubGFuOjg0NDMiLCJ1YnVudHUtMi5xZW11Lmxhbjo4NDQzIl0sInNlY3JldCI6IjliZjc3OTM3MDk0ZWJmMzVlNTFlMDY3ZGFmYTJiOTI4ZGFiYjdlMDMzNmQ3M2E3ZmRmYWRmMjAwMzU5N2I2OWIiLCJleHBpcmVzX2F0IjoiMjAyNi0wMi0xMVQxMzozNjoxMC42Njk4NDE4WiJ9
All existing data is lost when joining a cluster, continue? (yes/no) [default=no] yes
Choose "source" property for storage pool "local":
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: yes
config: {}
networks: []
storage_pools: []
storage_volumes: []
profiles: []
projects: []
cluster:
  server_name: ubuntu-3
  enabled: true
  member_config:
  - entity: storage-pool
    name: local
    key: source
    value: ""
    description: '"source" property for storage pool "local"'
  cluster_address: ubuntu-1.qemu.lan:8443
  cluster_certificate: |
    -----BEGIN CERTIFICATE-----
    MIIB6zCCAXCgAwIBAgIRAOt7X7eWVMvReGjd1dNJSN4wCgYIKoZIzj0EAwMwJjEM
    MAoGA1UEChMDTFhEMRYwFAYDVQQDDA1yb290QHVidW50dS0xMB4XDTI2MDIxMTEw
    MjAzMVoXDTM2MDIwOTEwMjAzMVowJjEMMAoGA1UEChMDTFhEMRYwFAYDVQQDDA1y
    b290QHVidW50dS0xMHYwEAYHKoZIzj0CAQYFK4EEACIDYgAE+rKZCP7zL8cjNIG6
    cQ+n8X5KCl4IVGqD0PcKXW8NZuDVqKxHr0ynlW1e2/fUq9ELhClOSdNtDCqqsgh7
    8XBJnvVjRon4E+u3zzuWRMo9GBHX8v5a0AOUgB1TMv2w8iW4o2IwYDAOBgNVHQ8B
    Af8EBAMCBaAwEwYDVR0lBAwwCgYIKwYBBQUHAwEwDAYDVR0TAQH/BAIwADArBgNV
    HREEJDAiggh1YnVudHUtMYcEfwAAAYcQAAAAAAAAAAAAAAAAAAAAATAKBggqhkjO
    PQQDAwNpADBmAjEA+/mDQCjVvlgaGyWvB5t6pJBfR+RvwkRk/7P6lb6qm7x203xW
    m+/pc+2DzLZY6HJfAjEA/LWFYYQ5/XTQN0Vv7B2wQkVjOhcGewC8uTX2S58USLxp
    eNePpqw4W8YlwgEDdkQ+
    -----END CERTIFICATE-----
  server_address: ubuntu-3.qemu.lan:8443
  cluster_password: ""
  cluster_token: ""
  cluster_certificate_path: ""
```
