NPFchan API
==========

## Welcome ##

Welcome to NPFchan's read-only JSON API documentation.

This API works at every vichan/NPFchan-based board, for example 8ch.net, and at a few Tinyboard-based ones (ask your admin to enable it).

JSON representations of threads and indexes are exposed at the following URLs:

http(s):///`siteurl`/`board`/res/`threadnumber`.json  
http(s)://`siteurl`/`board`/`pagenumber`.json (0 is main index, unlike on 4chan, which is 1-based)

A JSON representation of all thread OPs (and the replies shown on indexes) from an individual board can be found at the following URL:

http(s)://`siteurl`/`board`/catalog.json

And just the thread IDs, their modification times, and respective pages can be found here:

http(s)://`siteurl`/`board`/threads.json

A list of boards is exposed at the following URL: (nb. this is not yet implemented, it may work on individual sites)

http(s)://`siteurl`/boards.json

CORS may be supported, on discretion of board owners.

Supported request methods are: GET, HEAD, OPTIONS

*This guide was last updated May 26, 2017.*

### Posts Object ####

Incompatibilities with 4chan API are marked with (!).

Not yet implemented features, but marked for implementation, are marked with (ni).

Custom NPFchan/vichan additions, as compared to 4chan API, are marked with (NEW).

| **attribute**   | **value**      | **description**      | **possible values**                        | **example value**     |
|:----------------|:---------------|:---------------------|:-------------------------------------------|:----------------------|
| `no`            | `integer`      | Post number          | 1-9999999999999                            | `9001`                |
| `resto`         | `integer`      | Reply to             | 0 (is a thread OP), 1-9999999999999        | `0`                   |
| `sticky`        | `integer`      | Stickied thread?     | 0 (no), 1 (yes)                            | `1`                   |
| `closed`        | `integer`      | Closed thread?       | 0 (no), 1 (yes)                            | `1`                   |
| `archived`      | does not exist here (!) |
| `now`           | does not exist here (!) |
| `time`          | `integer`      | UNIX timestamp       | UNIX timestamp                             | `1344570123`          |
| `name`          | `string`       | Name                 | text                                       | `moot`                |
| `trip`          | `string`       | Tripcode             | text (format: !tripcode!!securetripcode)   | `!Ep8pui8Vw2`         |
| `id`            | `string` (ni)  | ID                   | text (8 characters), Mod, Admin, Developer | `Admin`               |
| `capcode`       | `string`       | Capcode              | none, mod, admin, admin_highlight, developer | `admin`             |
| `country`       | `string`       | Country code         | text (2 characters, ISO 3166-1 alpha-2), XX (unknown) | `XX`       |
| `country_name`  | `string`       | Country name         | text                                       | `Unknown`             |
| `sub`           | `string`       | Subject              | text                                       | `This is a subject`   |
| `com`           | `string`       | Comment              | text (includes escaped HTML)               | `This is a comment`   |
| `tim`           | `string` (!)   | Renamed filename     | UNIX timestamp + microseconds              | `1344402680740`       |
| `filename`      | `string`       | Original filename    | text                                       | `OPisa`               |
| `ext`           | `string`       | File extension       | .jpg, .png, .gif, .pdf, .swf, .webm        | `.jpg`                |
| `fsize`         | `integer`      | File size            | 1-8388608                                  | `2500`                |
| `md5`           | `string`       | File MD5             | text (24 character, packed base64 MD5 hash)| `NOetrLVnES3jUn1x5ZPVAg==` |
| `w`             | `integer`      | Image width          | 1-10000                                    | `500`                 |
| `h`             | `integer`      | Image height         | 1-10000                                    | `500`                 |
| `tn_w`          | `integer`      | Thumbnail width      | 1-250                                      | `250`                 |
| `tn_h`          | `integer`      | Thumbnail height     | 1-250                                      | `250`                 |
| `filedeleted`   | `integer` (ni) | File deleted?        | 0 (no), 1 (yes)                            | `0`                   |
| `spoiler`       | `integer` (ni) | Spoiler image?       | 0 (no), 1 (yes)                            | `0`                   |
| `custom_spoiler`| does not exist here (!) |
| `omitted_posts` | `integer`      | # replies omitted    | 1-10000                                    | `33`                  |
| `omitted_images`| `integer`      | # image replies omitted | 1-10000                                 | `21`                  |
| `replies`       | `integer`      | # replies total      | 0-99999                                    | `231`                 |
| `images`        | `integer`      | # images total       | 0-99999                                    | `132`                 |
| `bumplimit`     | does not exist here (!) |
| `imagelimit`    | does not exist here (!) |
| `capcode_replies` | does not exist here (!) |
| `last_modified` | `integer`      | Time when last modified | UNIX timestamp                          | `1344571233`          |
| `tag`           | does not exist here (!) |
| `semantic_url`  | does not exist here (!) |

**Note the following attributes are optional:**  
`sticky` `closed` `archived` (only displays on OPs when true)  
`id` (only displays when board has DISPLAY_ID set)  
`name` (only displays if name is present, which is always unless there is a blank name and tripcode)  
`trip` (only displays if tripcode is present)  
`sub` (only displays if subject is present)  
`com` (only displays if comment is present)  
`capcode` (only displays when using a capcode)  
`country` `country_name` (only displays when board uses country flags)  
`filename` (only displays when image uploaded)  
`ext` (only displays when image uploaded)  
`fsize` (only displays when image uploaded)  
`w` (only displays when image uploaded)  
`h` (only displays when image uploaded)  
`tn_w` (only displays when image uploaded)  
`tn_h` (only displays when image uploaded)  
`filedeleted` (only displays when image uploaded)  
`spoiler` (only displays when image uploaded)  
`omitted_posts` (only displays on OPs on index pages)  
`omitted_images` (only displays on OPs on index pages)  
`replies` (only displays on OPs)  
`images` (only displays on OPs)  
`last_modified` (only displayed in threads.json, and includes replies, deletions, and sticky/closed changes)  

### Where are the files? ###

Boards: http(s)://`siteurl`/`board`/  
Indexes: http(s)://`siteurl`/`board`/`[1-10]`.html (# of pages varies per board, directory root is page 1)  

Threads: http(s)://`siteurl`/`board`/res/`resto`.html  
Replies: http(s)://`siteurl`/`board`/res/`resto`.html#p`no`  

Images: http(s)://`siteurl`/`board`/src/`tim`.`ext`  
Thumbnails: http(s)://`siteurl`/`board`/src/`tim`s.jpg  

Spoiler image: http(s)://`siteurl`/static/spoiler.png  

File deleted: http(s)://`siteurl`/static/deleted.png 

Country flags: http(s)://`siteurl`/static/flags/`country`.png

### Examples ###

To view a pretty-printed version of our thread, index, and catalog JSON, use [JSONLint](http://jsonlint.com).
