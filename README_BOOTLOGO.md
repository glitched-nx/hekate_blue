# hekate - Bootlogo

Das Bootlogo kann beliebig groß sein mit einem Maximum von 720 x 1280 Pixeln.

Wenn es kleiner als 720 x 1280 ist, wird es automatisch zentriert und der Hintergrund nimmt die Farbe des ersten Pixels an.

Der Prozess besteht darin, ein Landschaftsbootlogo zu erstellen und es dann um 90 Grad gegen den Uhrzeigersinn zu drehen.

Schließlich ist das unterstützte Format ein 32-Bit (ARGB) BMP. Klassische 24-Bit (RGB) BMPs werden aus Leistungsgründen nicht unterstützt.

## Konfiguration

Wenn ein Booteintrag einen benutzerdefinierten Logopfad angibt (`logopath=`), wird dieser geladen.

Wenn das oben Genannte nicht gefunden wird oder das Format nicht korrekt ist, wird versucht, `bootloader/bootlogo.bmp` zu laden.
Wenn dies nicht gefunden wird, wird das Standard-Hekate-Logo verwendet.

(`bootloader/bootlogo.bmp` ist im Grunde wie ein globales Bootlogo.)
