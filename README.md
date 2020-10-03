# ffprobewaarden
Toont een of meer eigenschappen van een audio- of video-bestand

## Gebruik:

    ffprobewaarden [u|[0-9]+|(a|v|V|s)[:[0-9]+]] alles|all|naam[,naam]... mediabestand
- u | [0-9]+ | (a|v|V|s)[:[0-9]+] : optioneel, selecteer type stream, of specifieke stream van dat type
  - u : alle streams met 'usable??' configuration
  - 9 : stream 9
  - a : alle audiostreams
  - v:0 : 1ste videostream
  - v:1 : 2de videostream
  - V : hoofd-videostream
  - s : alle ondertitelstreams

   Als geen stream gekozen wordt, worden de gekozen waarden van het container
    format getoond; als echter in dit geval alle waarden gevraagd worden, worden
    zowel al die van alle streams als al die van het container format getoond.
- alles|all|naam[,naam]... : toon alle waarden of enkel de gekozen waarden van
  de gekozen streams en/of het container format
  - elke naam kan voorafgegaan worden door een subdirectory zoals "TAG:" of
    DISPOSITION: , b.v. `codec_name,TAG:language` (subdirectory mag in kleine letters)
  - als slechts 1 naam gevraagd wordt, wordt enkel zijn waarde getoond, anders is
    het formaat `naam=waarde` of b.v. `TAG_language=waarde` (bemerk: ':' is vervangen door '_')
  - voeg een komma toe voor of na 1 enkele naam, om toch het formaat `naam=waarde`
    te gebruiken (ffprobe verdraagt dat blijkbaar)
- de gevormde ffprobe-opdracht wordt getoond op `stderr`

## Vereist:
bash >= 4.3, ffprobe, sed, cat

## Voorbeeld: toon alle beschikbare entries
    $ ffprobewaarden alles film.mp4

## Voorbeeld: toon alle beschikbare entries voor de 1ste video stream
    $ ffprobewaarden v:0 alles film.mp4

## Voorbeeld: toon de bit_rate van het container format
    $ ffprobewaarden bit_rate film.mp4

## Voorbeeld: zet codec van echte videostream in variable vc:
    $ vc=$(ffprobewaarden V codec_name film.mp4)

## Voorbeeld: zet sample rate van alle audio streams in array ar:
    $ ar=($(ffprobewaarden a sample_rate film.mp4))

## Voorbeeld: zet variabelen voor een aantal kenwaarden van het hoofd-video-spoor, met  een onderscheidend prefix:
    $ unset video_width video_height video_codec_name video_codec_tag_string video_bit_rate
    $ eval $(ffprobewaarden V width,height,codec_name,codec_tag_string,bit_rate film.mp4 |
        sed -E 's/^/video_/' )

## [Meer ffprobe-tips](https://trac.ffmpeg.org/wiki/FFprobeTips)
