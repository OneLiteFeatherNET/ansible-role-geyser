# Geyser Ansible Role

This Ansible role installs and configures Geyser on Ubuntu and Debian systems.

## Requirements

- Ansible 2.1 or higher
- A target system with Ubuntu (focal, bionic, xenial) or Debian (bullseye, buster, stretch)
- [SDKman by Comcast](https://github.com/Comcast/ansible-sdkman)

## Installation

Add this role to your Ansible project:

```sh
ansible-galaxy install git+https://github.com/onelitefeathernet/ansible-role-geyser.git,geyser
```

## Usage

Create a playbook that uses the role. Example:

```yaml
---
- hosts: all
  roles:
    - role: geyser
```

## Variables

The following variables can be defined in your playbook to configure the role:

```yaml
geyser:
  java:
    memory: 1G
  user: geyser
  installation_path: /home/geyser/geyser
  name: geyser
  config:
    bedrock:
      port: 19132
      clone_remote_port: false
      motd1: "Geyser"
      motd2: "Another Geyser server."
      server_name: ""
      compression_level: 6
      enable_proxy_protocol: false
    remote:
      address: "onelitefeather.net"
      port: 25565
      auth_type: "floodgate"
      allow_password_authentication: true
      use_proxy_protocol: false
      forward_hostname: true
    saved_user_logins:
      - ThisExampleUsernameShouldBeLongEnoughToNeverBeAnXboxUsername
      - ThisOtherExampleUsernameShouldAlsoBeLongEnough
    floodgate_key_file: "key.pem"
    pending_authentication_timeout: 300
    command_suggestions: true
    ping_passthrough: true
    protocol_name_passthrough: true
    player_count_passthrough: true
    ping_passthrough_interval: 3
    forward_player_ping: true
    max_players: 100
    debug_mode: false
    allow_third_party_capes: true
    allow_third_party_ears: false
    show_cooldown: "title"
    show_coordinates: true
    disable_bedrock_scaffolding: false
    emote_offhand_workaround: "disabled"
    cache_images: 0
    allow_custom_skulls: true
    max_visible_custom_skulls: 128
    custom_skull_render_distance: 21
    add_non_bedrock_items: true
    above_bedrock_nether_building: true
    force_resource_packs: true
    xbox_achievements_enabled: false
    log_player_ip_addresses: true
    notify_on_new_bedrock_update: true
    unusable_space_block: "minecraft:barrier"
    metrics_enabled: true
    scoreboard_packet_threshold: 20
    enable_proxy_connections: false
    mtu: 1400
    use_direct_connection: true
    disable_compression: true
```

## Handlers

The role defines the following handlers:

```yaml
---
- name: Start {{geyser.name}}
  systemd:
    name: {{geyser.name}}
    state: started
    enabled: yes
    daemon_reload: yes
- name: Restart {{geyser.name}}
  systemd:
    name: {{geyser.name}}
    state: restarted
    daemon_reload: yes
```

## License

This project is licensed under the MIT License. For more information, see the LICENSE file.