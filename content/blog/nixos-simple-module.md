+++
title = "Modularazing NixOS configuration was simplier than expected"
date = 2026-08-07
+++

<!-- Petit résumé de quelques heures de bidoullage avec NixOS que j'ai récement streamé.
(Pas la peine de les regarder, ils ne sont pas très intéressant) -->

<div style="margin-left:auto;margin-right:auto;width:880px;">
<iframe width="420" height="315" src="https://www.youtube.com/embed/vPJnFx06V6I">
</iframe>
<iframe width="420" height="315" src="https://www.youtube.com/embed/1nUddDkvuBQ">
</iframe>
</div>

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
