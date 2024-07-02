# hekate - Bootlogo

Das Bootlogo kann jede Größe bis zu einem Maximum von 720 x 1280 haben.

Ist es kleiner als 720 x 1280, wird es automatisch zentriert und der Hintergrund nimmt die Farbe des ersten Pixels an.

Der Prozess besteht darin, ein Landschafts-Bootlogo zu erstellen und dieses dann um 90 Grad gegen den Uhrzeigersinn zu drehen.

Zuletzt wird das unterstützte Format als 32-Bit (ARGB) BMP angegeben. Klassische 24-Bit (RGB) BMPs werden aus Leistungsgründen nicht unterstützt.

## Konfiguration

Wenn ein Boot-Eintrag einen benutzerdefinierten Logo-Pfad (`logopath=`) angibt, wird dieses geladen.

Wenn das oben Genannte nicht gefunden wird oder das Format nicht korrekt ist, wird versucht, `bootloader/bootlogo.bmp` zu laden.
Wird dies nicht gefunden, wird das Standard-Hekate-Logo verwendet.

(`bootloader/bootlogo.bmp` fungiert im Grunde wie ein globales Bootlogo.)
