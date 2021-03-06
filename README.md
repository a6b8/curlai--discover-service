<img src="./assets/logo.png" width="200px">

# RSS Discover Service

## Quickstart (Heroku)
1. Create your Heroku Instance<br>
<a href="https://heroku.com/deploy?template=https://github.com/a6b8/curlai--discover-service">
  <img src="https://www.herokucdn.com/deploy/button.svg" alt="Deploy">
</a><br>

2. Setup Environment Variables<br>
  ```MULTIPLICATOR : [Int]```<br>
  ```DEBUG : [boolean]```<br>

3. Execute command in terminal: ```ruby test.rb```
   - [x] Set Server<br>
   - [x] Set Video Id<br>
   - [x] Set Multiplicator<br>

## Routes
| Nr | Type | Route | Parameter | Return |
| --- | --- | --- |  --- | --- | 
| 1 | yt | /discover/yt/watch/```video_id```?access=```access``` | Video ID (String), Access Token (Int) | Channel ID, Channel Name, RSS Feed | 

**Response**
1. yt
```json
{
    "video": {
        "id": "VIDEO_ID",
    },
    "channel": {
        "id": "CHANNEL_ID",
        "name": "CHANNEL_NAME"
    },
    "rss": {
      "url": "RSS_URL"
    }
}
```

## Use Service in Spreadsheets
Find RSS by Video URL

**1. Install ```ImportJSON``` [bradjasper/github](https://github.com/bradjasper/ImportJSON)**

**2. Copy into Spreadsheet**
| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| **Multiplicator:** | 42  |
| **Date:** | =NOW()  |
| **Date Copy:** | Copy Date: Right Mouse Click -> Values Only]  |
| **Api:** | https://api.example.com |
| **Route** | /discover/yt/watch/ |  |   |   |   |   | 
| NR | VIDEO URL | REQUEST | VIDEO ID |	CHANNEL ID | CHANNEL NAME | RSS URL |
| =IF(A6="NR",1,A6+1) | [YOUR VIDEO URL] | =CONCATENATE( $B$4, $B$5, INDEX( SPLIT( B7,"?v=","" ), 2 ),"?","access=", FLOOR( ( YEAR( $B$3 ) - MONTH( $B$3 ) + DAY( $B$3 ) ) * $B$1 ) ) | =INDEX( ImportJSON( C7 ), 2 ) | | | | |
