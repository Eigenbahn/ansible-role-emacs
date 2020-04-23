eigenbahn.emacs
=========

Install [GNU Emacs](https://www.gnu.org/software/emacs/), either from package manager of compiling from source.

When compiling from source, the [bgex patch](http://umiushi.org/~wac/bgex/) ([source](https://github.com/wachikun/emacs_bgex)) can be enabled to set background pictures.

Requirements
------------

Any Debian-based linux system.


Role Variables
--------------

The main variables are:

 - `emacs_version`: version to install.
 - `emacs_install_method`: either `package` to install from package manager or `compile` (default) to install from source
 - `emacs_enable_user_service`: if set to `yes` (not default) and `emacs_version` >= 26.1, enable the systemd user service for user `emacs_enable_user_service_for_users`
 - `emacs_enable_user_service_for_users`: users for who to enable the systemd user service

When `emacs_install_method` is `compile`, options/flags can be set using the following:

 - `emacs_nox`: when `yes` (not default), compiles without X server support. Ideal for servers.
 - `emacs_modules`: when `yes` (default), compiles with modules support (if `emacs_version` >= 25.1)
 - `emacs_configure_opts`: raw string allowing to set compile options/flags.

Setting `emacs_apply_patch_bgex` to `yes` (not default) also applies the `bgex` patch.

Additionally in case of `compile`, sources get installed by default. You can control it like so:

 - `emacs_install_src`: if set to `yes` (default) install emacs sources at location `emacs_src_parent_folder`
 - `emacs_src_parent_folder`: where to install emacs src

Please note that the role has a mechanism to not skip all tasks if the `emacs` binary with version `{{ emacs_version }}` is found on the system.

If for any reason you'd like to re-install it (e.g. due to upstream changes in the code or compile it differently) you can force the reinstallation by setting var `emacs_force_reinstall` to `yes`.

Likewise, when `compile`, temporary source folder is not re-downloaded if found in the temp folder. To force re-downloading them, set `emacs_force_build` to `true`.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: eigenbahn.emacs
           emacs_install_method: compile
           emacs_version: 26.2
           emacs_modules: yes
           emacs_apply_patch_bgex: yes
           emacs_enable_user_service: yes
           emacs_enable_user_service_for_users:
             - potatoman
             - avocadogirl

License
-------

MIT

Author Information
------------------

Jordan Besly [@p3r7](https://github.com/p3r7) ([blog](https://www.eigenbahn.com/)).
