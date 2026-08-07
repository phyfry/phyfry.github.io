+++
title = "Modularazing NixOS configuration was simplier than expected"
description = "FOOBAR"
date = 2026-08-07
+++

<!-- Petit résumé de quelques heures de bidoullage avec NixOS que j'ai récement streamé.
(Pas la peine de les regarder, ils ne sont pas très intéressant) -->

## TODO

<p class="filename"><code>flake.nix</code></p>

```nix
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-26.05";
  };
  outputs =
    inputs@{ self, nixpkgs, ... }:
    {
      nixosConfigurations.homeserver = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
          ./hardware-configuration.nix
          ./container-service1.nix
          ./container-service2.nix
        ];
      };
    };
}
```

## Flake target

<p class="filename"><code>flake.nix</code></p>

```nix
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-26.05";
  };
  outputs =
    inputs@{ self, nixpkgs, ... }:
    {
      nixosConfigurations.homeserver = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
          ./hardware-configuration.nix
          ./container-service1.nix
          ./container-service2.nix
        ];
      };
      nixosConfigurations.testvm = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
          ./service-to-test.nix
        ];
      };
    };
}
```

```bash
# Build the configuration
nixos-rebuild build --flake .#homeserver --verbose
# Build the virtual machine
nixos-rebuild build-vm --flake .#testvm --verbose
# Launch the virtual machine with QEMU
./result/bin/run-vmname-vm
```

## simple module

## Sidetrack by packages

## QEMU and networking

## Building Docker container

## Streams Archive

You can find the streams I was doing while tinkering with NixOS below. I discourage you from watching them, they are not entertaining.

<div style="margin-left:auto;margin-right:auto;width:880px;">
<iframe width="420" height="315" src="https://www.youtube.com/embed/vPJnFx06V6I">
</iframe>
<iframe width="420" height="315" src="https://www.youtube.com/embed/1nUddDkvuBQ">
</iframe>
</div>
