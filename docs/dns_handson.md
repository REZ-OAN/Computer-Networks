# Detailed Work flow Of DNS

## Prerequisite
 - [Wireshark (network protocol analyzer)](https://github.com/REZ-OAN/Computer-Networks/blob/main/docs/wireshark_installation_process.md)

## Step-1 (Checking the local DNS)

To check this on linux, the **DNS server** configuration is set to `/etc/resolv.conf` file. 
```
cat /etc/resolv.conf | grep "nameserver"
```
Execution of this command will list the `nameserver` it lookup locally. In my case the output :

![local_nameserver](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/007.local_nameserver.png)

## Step-2 (Clear the cache from the `browser`)

Because DNS is much more efficient we need to be careful about the cache. To verify the whole process we need to remove the cache from our browsers. (I have demonstrating using chrome). Navigate to this url to clear the browser cache `chrome://net-internals/#dns`.

![removing_cache_from_browser](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/008.removing_cache.png)

## Step-3 (Clear the cache from you `localhost`)

To remove the cache from the localhost :

### Using `resolvectl`
```
sudo resolvectl flush-caches
```
### Using `NetworkManager`
```
sudo systemctl restart NetworkManager
```
## Step-4 (Remove cache from `local nameserver`)
As you have shown in the [Step-1](#step-1-checking-the-local-dns) that our localhost it self working as a nameserver, for this we have to clear the cache of it. Immediately after clearing the cache, start **Wireshark** to quickly capture any new DNS requests that populate the cache within milliseconds. This ensures you capture the relevant traffic for analysis.
To remove cache from **local nameserver**
```
sudo systemctl restart NetworkManager
```
## Step-5 (WireShark Analyzer)
When you write the command in your terminal from [Step-4](#step-4-remove-cache-from-local-nameserver), aside you open wireshark from you terminal:
```
sudo wireshark
```
Then open analyzer for the `interface` which is connected to internet (in my case it is `wlp3s0`). And on your browser open a new tab and write any of url to navigate.

Now do three things  quickly: 
 - First execute the command from [Step-4](#step-4-remove-cache-from-local-nameserver)
 - Second restart the wireshark analyzer 

![restart_analyzer](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/009.restart_analyzer.png)

 - Third Navigate to the written url

Now if the url loaded in your browser stop the analyzer (click on the red colored pause button). You will see many protocols are there, but we need only the DNS protocol results. 

To get only the DNS protocol results

![show_dns_protocol_results](https://github.com/REZ-OAN/Computer-Networks/blob/main/images/010.show_only_dns.png)

