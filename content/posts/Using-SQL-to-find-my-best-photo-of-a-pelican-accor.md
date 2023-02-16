
---
    title: Using-SQL-to-find-my-best-photo-of-a-pelican-accor
    date: 2021-01-01    
    draft: true
    tags: []
---
# Using-SQL-to-find-my-best-photo-of-a-pelican-accor# Using SQL to find my best photo of a pelican according to Apple Photos
Created: May 22, 2020 8:02 PM
URL: https://simonwillison.net/2020/May/21/dogsheep-photos/
According to the Apple Photos internal SQLite database, this is the most aesthetically pleasing photograph I have ever taken of a pelican:
!
[Using%20SQL%20to%20find%20my%20best%20photo%20of%20a%20pelican%20accor%202abe187079964d1284b0f800b448a8e2/cbfe463f1a67e37a1d36c5db44f0159ef6f86a0d64a987b129b63b52e555f1af.jpeg](Using%20SQL%20to%20find%20my%20best%20photo%20of%20a%20pelican%20accor%202abe187079964d1284b0f800b448a8e2/cbfe463f1a67e37a1d36c5db44f0159ef6f86a0d64a987b129b63b52e555f1af.jpeg)
Here’s the SQL query that found me my best ten pelican photos:
```
select
sha256,
ext,
uuid,
date,
ZOVERALLAESTHETICSCORE
from
photos_with_apple_metadata
where
uuid in (
select
uuid
from
labels
where
normalized_string = 'pelican'
)
order by
ZOVERALLAESTHETICSCORE desc
limit
10
```
You can [try it out here](https://dogsheep-photos.dogsheep.net/public?sql=select%0D%0A++json_object%28%0D%0A++++%27img_src%27%2C%0D%0A++++%27https%3A%2F%2Fphotos.simonwillison.net%2Fi%2F%27+%7C%7C+sha256+%7C%7C+%27.%27+%7C%7C+ext+%7C%7C+%27%3Fw%3D600%27%0D%0A++%29+as+photo%2C%0D%0A++sha256%2C%0D%0A++ext%2C%0D%0A++uuid%2C%0D%0A++date%2C%0D%0A++ZOVERALLAESTHETICSCORE%0D%0Afrom%0D%0A++photos_with_apple_metadata%0D%0Awhere%0D%0A++uuid+in+%28%0D%0A++++select%0D%0A++++++uuid%0D%0A++++from%0D%0A++++++labels%0D%0A++++where%0D%0A++++++normalized_string+%3D+%3Alabel%0D%0A++%29%0D%0Aorder+by%0D%0A++ZOVERALLAESTHETICSCORE+desc%0D%0Alimit%0D%0A++10&label=pelican) (with some extra [datasette-json-html](https://github.com/simonw/datasette-json-html/blob/master/README.md#images) magic to display the actual photos).
[Using%20SQL%20to%20find%20my%20best%20photo%20of%20a%20pelican%20accor%202abe187079964d1284b0f800b448a8e2/a444857c4ac71ceae6af5192c8acc5ac35934ed589259136df0ed11295dbb085.jpeg](Using%20SQL%20to%20find%20my%20best%20photo%20of%20a%20pelican%20accor%202abe187079964d1284b0f800b448a8e2/a444857c4ac71ceae6af5192c8acc5ac35934ed589259136df0ed11295dbb085.jpeg)
### How this works
Apple Photos keeps photo metadata in a SQLite database.
### An aside: Why I love Apple Photos
The Apple Photos app—on both macOS and iOS—is in my opinion Apple’s most underappreciated piece of software.
### Querying the Apple Photos SQLite database
If you run Apple Photos on a Mac (which will synchronize with your phone via iCloud) then most of your photo metadata can be found in a database file that lives here:
```
~/Pictures/Photos\ Library.photoslibrary/database/Photos.sqlite
```
Mine is 752MB, for aroud 40,000 photos.
Here’s a full list, each one linking to my public photos sorted by that score:
- [ZBEHAVIORALSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZBEHAVIORALSCORE)
- [ZFAILURESCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZFAILURESCORE)
- [ZHARMONIOUSCOLORSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZHARMONIOUSCOLORSCORE)
- [ZIMMERSIVENESSSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZIMMERSIVENESSSCORE)
- [ZINTERACTIONSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZINTERACTIONSCORE)
- [ZINTERESTINGSUBJECTSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZINTERESTINGSUBJECTSCORE)
- [ZINTRUSIVEOBJECTPRESENCESCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZINTRUSIVEOBJECTPRESENCESCORE)
- [ZLIVELYCOLORSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZLIVELYCOLORSCORE)
- [ZLOWLIGHT](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZLOWLIGHT)
- [ZNOISESCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZNOISESCORE)
- [ZPLEASANTCAMERATILTSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTCAMERATILTSCORE)
- [ZPLEASANTCOMPOSITIONSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTCOMPOSITIONSCORE)
- [ZPLEASANTLIGHTINGSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTLIGHTINGSCORE)
- [ZPLEASANTPATTERNSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTPATTERNSCORE)
- [ZPLEASANTPERSPECTIVESCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTPERSPECTIVESCORE)
- [ZPLEASANTPOSTPROCESSINGSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTPOSTPROCESSINGSCORE)
- [ZPLEASANTREFLECTIONSSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTREFLECTIONSSCORE)
- [ZPLEASANTSYMMETRYSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZPLEASANTSYMMETRYSCORE)
- [ZSHARPLYFOCUSEDSUBJECTSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZSHARPLYFOCUSEDSUBJECTSCORE)
- [ZTASTEFULLYBLURREDSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZTASTEFULLYBLURREDSCORE)
- [ZWELLCHOSENSUBJECTSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZWELLCHOSENSUBJECTSCORE)
- [ZWELLFRAMEDSUBJECTSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZWELLFRAMEDSUBJECTSCORE)
- [ZWELLTIMEDSHOTSCORE](https://dogsheep-photos.dogsheep.net/public/photos_with_apple_metadata?_sort_desc=ZWELLTIMEDSHOTSCORE)
I’m not enormously impressed with the results I get from these.
It took [some work](https://github.com/dogsheep/dogsheep-photos/issues/16) to figure out how to match those labels with their corresponding photos, mainly because the `psi.sqlite` database stores photo UUIDs as a pair of signed integers whereas the `Photos.sqlite` database stores a UUID string.
