# Afanasy Pools Addin <img src="https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/afpools2.png" align="right" width="128">
A provisionally [CGRU](http://cgru.info/) pools implementation. It's not the official implementation. It's more of a workaround.

With the **Afanasy Pools Addin** you can create pools and assign clients to them. When you create an Afanasy job, whether using the [AfStarter](http://cgru.info/afstarter) or a [software plugin](http://cgru.info/software/blender), you can always specify a pool for rendering.

The pools are more a superficial solution and are not stored in the **Afanasy's code**, so you don't see any pools in the [Afanasy Web GUI](http://cgru.info/afanasy/gui#web) or in the [Afanasy Qt GUI](http://cgru.info/afanasy/gui#page_top).

[CGRU - Afanasy Render Manager](http://cgru.info/afanasy/afanasy)

## Why this project?

On the [**CGRU Roadmap**](http://cgru.info/roadmap) a pool support is planned for the future. But since we needed a provisional pool solution in one project, we developed one ourselves which works through a workaround.

The project still has its weaknesses in some places, because it has been developed rapidly.
If there are bugs, just create an [issue on Github](https://github.com/laurence-trippen/Afanasy-Pools-Addin/issues).

## How does it works?

For every Afanasy render job you can specify a hosts exclude mask.
In this mask individual render clients can be excluded from a job by a [regular expression](https://en.wikipedia.org/wiki/Regular_expression).

Let's assume we have a render farm with five render clients.
```
pc-01, pc-02, pc-03, pc-04 and pc-05
```
With this regular expression, we can, for example, exclude these three render clients from a job.
```Regular Expression
pc-01|pc-02|pc-04
```
This means that the job is executed on the two render clients **pc-03** and **pc-05**.

The hosts exclude mask can be used to create pools indirectly.
For example, let's take the five render clients from above.
Let's define a pool where **pc-01** and **pc-03** are contained.

From this pool the following mask would have to be generated, so that on the
Render Farm, the job can only be executed with **pc-01** and **pc-03**.

Generated mask to run job on renderfarm with **pc-01** and **pc-03**.
```Regular Expression
pc-02|pc-04|pc-05
```

![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/plan.jpg?raw=true)

### Pool emulation by hosts exclude mask.

```python
def get_excluded_hostnames(all_clients, pool_clients):
  excluded = []
  for client in all_clients:
    if not client in pool_clients:
      excluded.append(client)
  return excluded
```

## Afanasy Pool Manager

![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/keeperaddin.jpg?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/mainview.JPG?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/createpool.JPG?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/deletepool.JPG?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/addclients.JPG?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/networkscan.JPG?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/addhostname.JPG?raw=true)

## Blender Pool Integration
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/blender-plugin-pools.jpg?raw=true)
![](https://github.com/laurence-trippen/Afanasy-Pools-Addin/blob/master/Preview/blender-plugin-select-pool.jpg?raw=true)
