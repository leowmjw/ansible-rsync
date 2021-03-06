ansible-rsync
=============

## synchronize


An Ansible action plugin using rsync to make synchronizing a file paths in your playbooks quick and easy. Of course you could just use the command action to call rsync yourself, but you also have to add a fair number of boilerplate options and host facts. You still may need to call rsync directly via `command` or `shell`. The synchronize action is meant to do common things with `rsync` easily. It does not provide access to the full power of rsync. 

<table>
<tr>
<th class="head">parameter</th>
<th class="head">required</th>
<th class="head">default</th>
<th class="head">choices</th>
<th class="head">comments</th>
</tr>
<tr>
<td>dest</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>Path on the destination machine that will be synchronized from the source; The path can be absolute or relative.</td>
</tr>
<tr>
<td>src</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>Path on the source machine that will be synchronized to the destination; The path can be absolute or relative.</td>
</tr>
<tr>
<td>verbosity</td>
<td>no</td>
<td></td>
<td><ul></ul></td>
<td>An integrater controling the amount of information returned during processing. The greater the value the more information rsync will report back. See the <code>-v, --verbose</code> option of the rsync man page for details. If verbosity is not defined or a value of 0 is assumed, the <code>--quiet</code> option is passed and information is supressed.</td>
</tr>
<tr>
<td>mode</td>
<td>no</td>
<td>push</td>
<td><ul><li>push</li><li>pull</li></ul></td>
<td>Specify the direction of the synchroniztion. In push mode the localhost or delgate is the  source; In pull mode the inventory hostname in context is the source.</td>
</tr>
<tr>
<td>delete</td>
<td>no</td>
<td>no</td>
<td><ul><li>yes</li><li>no</li></ul></td>
<td>Delete files that don't exist (after transfer, not before) in <code>src</code> path.</td>
</tr>
<tr>
<td>rsync_path</td>
<td>no</td>
<td></td>
<td></td>
<td>Specify rsync to run on the remote machine. See <code>--rsync-path</code> on the rsync man page.</td>
</tr>
</table>

* Synchronization of src on the localhost to dest on the current inventory host

```
synchronize: src=some/relative/path dest=/some/absolute/path
```
* Synchronization of src path to dest path on the localhost

```
local_action: synchronize src=some/relative/path dest=/some/absolute/path
```
* Synchronization of src on the inventory host to the dest on the localhost.

```
synchronize: mode=pull src=some/relative/path dest=/some/absolute/path
```
* Synchronization of src on delegate to dest on the current inventory host

```
synchronize: src=some/relative/path dest=/some/absolute/path
  delegate_to: delegate.host

```
* Synchronize and delete files in dest on inventory host not found in src of localhost.

```
synchronize: src=some/relative/path dest=/some/absolute/path delete=yes
```
* Synchronize and return verbose information from the rsync transfer.

```
synchronize: src=some/relative/path dest=/some/absolute/path verbosity=1
```
* Synchronize with using an alternate rsync command. See --rsync-path on the rsync man page.

```
synchronize: src=some/relative/path dest=/some/absolute/path rsync_path="sudo rsync"
```
