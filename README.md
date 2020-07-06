# ffprobewaarden
Toont een of meer eigenschappen van een audio- of video-bestand

Gebruik:

    ffprobewaarden [(a|v|V|s)[:[0-9]+]] alles|all|entry[,entry]... mediabestand

    (a|v|V|s)[:[0-9]+] : selecteer een type stream, of een specifieke stream van dat type, b.v.
        a : alle audiostreams
        v:0 : 1ste videostream
        v:1 : 2de videostream
        V : hoofd-videostream
        s : alle ondertitelstreams
    - als geen stream gekozen wordt, worden de gekozen entries van elke stream EN van het container format getoond
    
    alles|all|entry[,entry]... : toon alle entries of enkel de gekozen entries van de gekozen streams en/of het container format
    - als slechts 1 entry gevraagd wordt, wordt enkel de waarde getoond, anders is het formaat "naam=waarde"
    - voeg een komma toe voor of na 1 enkele entry, om toch het formaat "naam=waarde" te gebruiken (ffprobe verdraagt dat blijkbaar)

## Voorbeeld: toon alle beschikbare entries
		ffprobewaarden alles film.mp4

## Voorbeeld: toon alle beschikbare entries voor de 1ste video stream
		ffprobewaarden v:0 alles film.mp4

## Voorbeeld: zet audio sample rate in variable ar:
	 	ar=$(ffprobewaarden a sample_rate film.mp4)
