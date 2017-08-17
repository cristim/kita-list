# Hacking a list of Kita contacts

I live in Berlin and I'm expecting a baby soon, ETA mid-November or exactly three
months from now. Considering the Kita(short for Kindergarten) application
'process' which I think is by far the thing Germans really suck at worst, even
surpassing their finance/banking system, I'm apparently already supposed to
start looking for a Kita place for the baby, well before birth, even though the
kid will stay for the first year at home.

So after a lot of procrastination, multiple arguments with my wife in which my
parenthood was questioned and after hearing horror stories from colleagues who
applied at 50+ kitas only to be ignored or rejected by most, I've finally
started gathering contact information into a Google Docs spreadsheet so I can
start calling them and arrange for a place on their never-ending waitinglists
within the next few days.

At first I started manually like any other Berlin parent, by searching on
http://kita.de, then I soon ended up on
https://www.bildung.berlin.de/Umkreissuche/ where I think the information is a
bit more detailed.

After browsing a few Kitas and entering a couple of rows in the spreadsheet, I
ended up browsing Kita websites made in the early '90s, back when Comic Sans and
airplane-Marquee was still a thing in web development (seriously, I'm not
kidding, just have a look [here](http://www.kirschkern-ev.de/) ), I got again
distracted from the boring work of filling data in spreadsheet cells, at least
for a while. I can't imagine how people can do this for a living, it turns out
this is still a thing people get paid for.

It was getting late and the target of getting at least a few dozens of Kitas
listed was really getting unachievable for today, I stepped off the parent shoes
and remembered that I'm actually an engineer doing automation for a living, so I
thought there should be a better way to do this.

So I started to look around and I eventually came up with some instructions for
generating the list of Kitas in my neighborohood with contact information and
details without filling hundreds of spreadsheet cells manually.

## Scraping a Kita list

1. Open https://www.bildung.berlin.de/Umkreissuche/ and perform a search of
   Kitas near your address. I used the second filter, which also allows setting
   a distance limit from the address.
1. Save the result as HTML, and put it somewhere where you can open it with a
   browser. I used nginx configured against my `public_html`, so moved it under
   `~/public_html/kita-list/`.
1. Install the awesome http://webscraper.io/ Chrome extension and watch the
   instructions video. You won't really need all of it since I put all the
   boring effort to configure it against the website, but it may still be
   educational to see it all.
1. I also needed to add a `localhost.local` entry into /etc/hosts because the
   webscraper extension doesn't accept localhost as a valid hostname.
1. Open http://localhost.local/~username/kita-list/list.html in Chrome once the
   extension is installed and go to the webscraper tab in the browser inspector.
1. Import my webscraper configuration you can find in the repo and tweak it to
   fully match your localhost URL (You will need to edit the sitemap metadata)
1. Run the scraper, and a few minutes later you'll have a list of dozens of
   Kitas ready to be saved into a CSV file.

If you have any issues or you have improvement suggestions,  feel free to
contact me on Gitter or send a pull request.

## Next steps

You can now dump the generated CSV in Google Docs and start contacting the kitas
one by one. You can at least quickly see if the address and the schedule are
matching your needs so you skip those which you don't like.

I hope this saves a few hours of boring work for someone out there. If you live
in Berlin and find this useful, I happily accept payments in Hefeweizen, my
preferred liquid currency :-)

Good luck at finding your Kita place!