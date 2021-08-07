+++
math = false 
meta = false
toc = false
author = "Royce"
title = "How to Install dapptools on an M1 Mac"
date = "2021-08-07"

+++

I ran in to some issues trying to install [dapptools](https://github.com/dapphub/dapptools) on my M1 MacBook Air. The project Readme.md helpfully explains that you have to run dapptools and the installer under Rosetta 2. But it took me a few tries to get it right and there wasn't a clear explanation of the complete steps, so recording those here.  

`dapptools` is a set of UNIX-style command line tools to interact with Ethereum contracts.

Particularly, I wanted to use the `seth` command line tool to interact with some contracts. I haven't run in to many issues installing tooling on my M1 MacBook Air, but following the basic installation in the dapptools Readme threw a bunch of errors. After looking back through again, I noticed the note about GHC compilation in Haskell on ARM architecture.

Now knowing that you have to install and run the program under a Rosetta 2 emualted x86 program was all well and good, but I didn't have any idea what that meant. Some searching later, I found a helpful tutorial on how to set up your Terminal profile to run Rosetta 2 instead of the default. Once the profile was set up, you have to both install Nix and run the dapptools installation script from the Rosetta 2 terminal. {{% marginnote %}}This note thanks to a bit of a frustration from successfully installing Nix under the ARM environment, then running in to errors when trying to install dapptools in the Rosetta 2 environment.{{% /marginnote %}}

Once the environment issues were sorted out the installation ran without a problem. 

So here are the full setps to install dapptools on an M1 Mac. 

1. Open Terminal, go to Prefrences and create a duplicate profile from your current set up. 
2. Rename the new profile and change the title in the Window tab of prefrences so that you know it is a Rosetta 2 terminal
3. Go to the Shell tab in prefrences and add the startup command (uncheck the "Run inside Shell" option) 
    ```sh 
    env /usr/bin/arch -x86_64 /bin/zsh --login
    ``` 
5. Open a new terminal with the Rosetta 2 profile you just created.     
6. Install Nix per the dapptools readme instructions: 
    ```sh
    # user must be in sudoers
    curl -L https://nixos.org/nix/install | sh

    # Run this or login again to use Nix
    . "$HOME/.nix-profile/etc/profile.d/nix.sh"
    ``` 
7. Install dapptools:
   ```sh
   curl https://dapp.tools/install | sh
   ```

That should do it. You will need to use the Rosetta 2 profile to run dapptools programs. You can run `seth --help` to check that it is working. Unless you have a local node running to use `seth` you still have to do some configuration of the `.sethrc` file to run queries. For me that meant setting up the RPC configuration to use a free Infura account.

```sh
# Add this line to your .sethrc with your API key
export ETH_RPC_URL=https://infura.io/v3/<API-KEY>
```