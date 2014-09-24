vichan API
==========

## Welcome ##

Welcome to vichan read-only JSON API documentation.

This API works at every vichan-based board, for example 8chan.co, and at a few Tinyboard-based ones (ask your admin to enable it).

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

Questions? Please e-mail [vichanapi@6irc.net](mailto:vichanapi@6irc.net).

*This guide was last updated September 24, 2014.*

### Posts Object ####

Incompatibilities with 4chan API are marked with (!).

Custom vichan additions, as compared to 4chan API, are marked with (NEW).

| **attribute**   | **value**      | **description**      | **possible values**                        | **example value**     |
|:----------------|:---------------|:---------------------|:-------------------------------------------|:----------------------|
| `no`            | `integer`      | Post number          | 1-9999999999999                            | `9001`                |
| `resto`         | `integer`      | Reply to             | 0 (is a thread OP), 1-9999999999999        | `0`                   |
| `sticky`        | `integer`      | Stickied thread?     | 0 (no), 1 (yes)                            | `1`                   |
| `closed`        | `integer`      | Closed thread?       | 0 (no), 1 (yes)                            | `1`                   |
| `archived`      | `integer`      | Archived thread?     | 0 (no), 1 (yes)                            | `1`                   |
| `now`           | `string`       | Date and time        | MM\/DD\/YY(Day)HH:MM (:SS on some boards), EST/EDT timezone  | `08\/08\/12(Wed)01:11`|
| `time`          | `integer`      | UNIX timestamp       | UNIX timestamp                             | `1344570123`          |
| `name`          | `string`       | Name                 | text                                       | `moot`                |
| `trip`          | `string`       | Tripcode             | text (format: !tripcode!!securetripcode)   | `!Ep8pui8Vw2`         |
| `id`            | `string`       | ID                   | text (8 characters), Mod, Admin, Developer | `Admin`               |
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
| `filedeleted`   | `integer`      | File deleted?        | 0 (no), 1 (yes)                            | `0`                   |
| `spoiler`       | `integer`      | Spoiler image?       | 0 (no), 1 (yes)                            | `0`                   |
| `custom_spoiler`| `integer`      | Custom spoilers?     | 1-99                                       | `3`                   |
| `omitted_posts` | `integer`      | # replies omitted    | 1-10000                                    | `33`                  |
| `omitted_images`| `integer`      | # image replies omitted | 1-10000                                 | `21`                  |
| `replies`       | `integer`      | # replies total      | 0-99999                                    | `231`                 |
| `images`        | `integer`      | # images total       | 0-99999                                    | `132`                 |
| `bumplimit`     | `integer`      | Bump limit met?      | 0 (no), 1 (yes)                            | `0`                   |
| `imagelimit`    | `integer`      | Image limit met?     | 0 (no), 1 (yes)                            | `1`                   |
| `capcode_replies` | `array`      | Capcode user replies?| array of capcode type and post IDs         | `{"admin":[1234,1267]}` |
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
`md5` (only displays when image uploaded)  
`w` (only displays when image uploaded)  
`h` (only displays when image uploaded)  
`tn_w` (only displays when image uploaded)  
`tn_h` (only displays when image uploaded)  
`filedeleted` (only displays when image uploaded)  
`spoiler` (only displays when image uploaded)  
`custom_spoiler` (only display on OPs, only displays when board has custom spoiler images)  
`omitted_posts` (only displays on OPs on index pages)  
`omitted_images` (only displays on OPs on index pages)  
`replies` (only displays on OPs)  
`images` (only displays on OPs)  
`bumplimit` (only displays on OPs when true)  
`imagelimit` (only displays on OPs when true)  
`capcode_replies` (only displays on /q/ when there are capcode user replies)  
`last_modified` (only displayed in threads.json, and includes replies, deletions, and sticky/closed changes)  
`tag` (only displays on /f/)  
`semantic_url` (only displays on OPs)

**Note about custom spoilers:**  
`custom_spoiler` describes the number of custom spoilers that exist for the specified board. If the number is `4`, it means that you can choose anywhere from 1 to 4. 
For our imageboard pages, the custom spoiler images changes every time a new post is made. If you are writing a browser add-on with auto-update 
functionality, you should first check the HTML to see if a custom spoiler has been posted, and use the same number, so when new spoiler posts come in, they match the pre-existing ones. 
If there are no custom spoilers already in a thread, you can just random whatever you'd like, since there is no need to match pre-existing ones.

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
