# Step #1
- add this input to your system flake

```
  nauka = {
     url = "git+file:///home/choom/Documents/nauka_flake";
     inputs.nixpkgs.follows = "nixpkgs";
   };
```

# Step #2
- add this to your system pkgs

```
   inputs.nauka.packages.${pkgs.stdenv.hostPlatform.system}.default
```

# Step #3
- add this to your configuration.nix

```
   services.displayManager.sessionPackages = [
     inputs.nauka.packages.${pkgs.stdenv.hostPlatform.system}.default
   ];
```

# Step #4
- rebuild your system

```
$ nix flake update
$ sudo nixos-rebuild switch --flake #or whichever flavor of this command you use to build your system
```

## Testing
- you can test if nauka installed properly with this command :
```
$ which nauka
```
