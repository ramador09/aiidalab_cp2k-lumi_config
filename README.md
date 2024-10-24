# SETTING UP AIIDALAB WITH CP2K ON LUMI-G

1. make sure you have an ssh key without password (!!) for use with LUMI and make sure it's registered to your account. more details can be found [here](https://docs.lumi-supercomputer.eu/firststeps/SSH-keys/#__tabbed_2_1).
2. add the enclosed `lumi-g.yml` and `cp2k-lumi.yml` files to your home directory on aiidalab. these files contain the configuration parameters to setup the aiidalab computer on lumi-g as well as setting up cp2k.
3. open the `lumi-g.yml` file and change the `work_dir` to your working directory. you might also need to change the path (and modify the permissions) for the `select_gpu.sh` file.
4. using the lumi-g.yml file, we first want to setup the computer. execute in the aiidalab terminal:
```
$ verdi computer setup --config lumi-g.yml
Default amount of memory per machine (kB).: !
```
5. now we want to configure the computer. execute in the terminal the first line below, and assuming everything is ok with your ssh key (stored in `/home/jovyan/.ssh/`) you should just be able to accept the default values, and shown here:
```
$ verdi -p default computer configure core.ssh lumi-g
Report: enter ? for help.
Report: enter ! to ignore the default and set no value.
User name [amadorra]:
Port number [22]:
Look for keys [Y/n]:
SSH key file [/home/jovyan/.ssh/id_ed25519]:
Connection timeout in s [60]:
Allow ssh agent [Y/n]:
SSH proxy jump []:
SSH proxy command []:
Compress file transfers [Y/n]:
GSS auth [False]:
GSS kex [False]:
GSS deleg_creds [False]:
GSS host [lumi.csc.fi]:
Load system host keys [Y/n]:
Key policy (RejectPolicy, WarningPolicy, AutoAddPolicy) [RejectPolicy]:
Use login shell when executing command [Y/n]:
Connection cooldown time (s) [30.0]:
Report: Configuring computer lumi-g for user aiida@localhost.
Success: lumi-g successfully configured for aiida@localhost
```
6. the computer is now configured. now we just need to setup cp2k. execute:
```
$ verdi code setup --config cp2k-lumi.yml
```
7. cp2k should hopefully now work properly. when submitting calculations via aiidalab, make sure the `# Tasks per node` is set to 8 and `# threads per task` is set to 7 (the number of nodes is freely selectable):

![Bildschirmfoto 2024-10-24 um 15 06 13](https://github.com/user-attachments/assets/be6ae24f-2de0-42e3-837e-cdfc6a8e1814)
