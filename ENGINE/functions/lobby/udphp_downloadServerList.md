``udphp_downloadServerList(...)``
--------------

###Description

**Detailed information in [Tutorial - Bonus 1 - An ONLINE lobby](tutorial/13_lobby).**

Download the list of servers from the master server.

global.udphp_downloadlist_refreshing will be set true.
It will be set false again if download is finished and 
**global.udphp_downloadlist** will contain a list of online servers then.
If download fails, global.udphp_downloadlist_refreshing will never reset.
It will fail, if the master server has the lobby disabled or is not
reachable.

Use the (optional) arguments to sort and filter the list.
Default sorting can be seen below under arguments.

Format of **global.udphp_downloadlist**:

```
ds_list:
 [0...] => ds_map:
           [ip]    => string
           [data1] => string
           [data2] => string
           [data3] => string
           [data4] => string
           [data5] => string
           [data6] => string
           [data7] => string
           [data8] => string
           [createdTime] => string -> can be converted to real
                            unix timestamp, time the server was created.
```

###Arguments
Name | type | description
---- | ---- | -----------
\[limit\] | string/real | The number of servers to return or EMPTY STRING if ALL servers should be returned (optional)
\[sortby\] | string | Field to sort the result by, this can be: date (filter by time created; DEFAULT), data1, data2, data3, data4, data5, data6, data7, data8 (optional)
\[sortby_dir\] | string | Sort ascending ("ASC") or descending ("DESC"; DEFAULT) (optional)
\[filter_data1\] | string | Only list servers that match this excact string for their first data string (the game name). Can be EMPTY STRING if you don't want to filter (optional)
\[filter_data2\] | string | See above; but for second data string (optional)
\[filter_data3\] | string | See above... (optional)
\[filter_data4\] | string | See above... (optional)
\[filter_data5\] | string | See above... (optional)
\[filter_data6\] | string | See above... (optional)
\[filter_data7\] | string | See above... (optional)
\[filter_data8\] | string | See above... (optional)

###Returns
Nothing