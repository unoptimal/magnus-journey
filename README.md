# Following Magnus Carlsen's chess journey

This is a sort of annotated biography of Magnus Carlsen's chess career alongside a chart of his ratings progression over time. The [FIDE rating data](https://ratings.fide.com/profile/1503014) was scraped using xRuiAlves's [FIDE rating scraper](https://github.com/xRuiAlves/fide-ratings-scraper), and the scrollytelling format comes from Connor Rothschild's [scrollytelling guide](https://www.connorrothschild.com/post/svelte-scrollytelling).

I admittedly did not do much actual "analysis", but I did reference Carlsen's [Wikipedia page](https://en.wikipedia.org/wiki/Magnus_Carlsen) and [Chess.com profile](https://www.chess.com/players/magnus-carlsen) to annotate his chess career.

## Skills, approaches

Scrollytelling (through Svelte + D3) is super cool, and I'm glad I was able to get into the weeds of how it works. I previously had done a project using [scrollama](https://github.com/russellsamora/scrollama) but that was plain Javascript and felt less satisfying than this one, where I was able to get a chart moving alongside the scroll. I also got more experience using [Chart.js](https://www.chartjs.org/) which is a cool library. 

## Improvements

Ideally, I wanted each section to have more data points and somehow work-in the context of where each section is relative to his overall rating graph (perhaps a mini-map or something to that effect).

I also wanted to explore how his career arc compared to his peers and the average chess player. Ambitiously I wanted to add a feature that would let the user input their own FIDE ID and see how it compares as well. (This exists on some chess websites already, but I still think it would be a cool thing to add.)

Oh! It's also not mobile-friendly or responsive at all. 