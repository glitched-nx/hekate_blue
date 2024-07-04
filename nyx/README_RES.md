# Nyx - Hintergrund - Symbole

Der Hintergrund für Nyx muss ein 1280 x 720 32-Bit BMP sein. Alpha-Blending wird berücksichtigt. Aus diesem Grund muss der Wert 0xFF sein, wenn ein fester Hintergrund erforderlich ist. Es gibt Websites, die das korrekte BMP erzeugen können.

Die unterstützten Symbole sind 192 x 192 32-Bit BMP. Du kannst Transparenz nach Belieben nutzen und schöne Mischungen mit dem Tastenhintergrund erstellen.

Zusätzlich wird das Symbol unter Verwendung von `icon={sd path}` eingefärbt, wenn der Name mit `_hue.bmp` endet. Das funktioniert nur gut, wenn das Symbol ein weißes Layout mit Transparenz ist.

Wenn `_nobox.bmp` verwendet wird, wird der Tastenhintergrund entfernt. Nützlich für Symbolthemen, die auf einen bestimmten Stil abzielen.

Eine Kombination aus beiden kann über das Suffix `_hue_nobox.bmp` aktiviert werden.

Die Standardsystemsymbole (`icon_switch.bmp` und `icon_payload.bmp`) können durch weiße Layouts mit Transparenz ersetzt werden. Sie können auch durch normale Symbole ersetzt werden, wenn folgende vorhanden sind: `icon_switch_custom.bmp` und/oder `icon_payload_custom.bmp`.

## Wie zu konfigurieren

Der Hintergrund muss nach /bootloader/res/background.bmp

Die Symbole können entweder über `[boot entries names]` -> `boot entries names.bmp` oder durch Verwendung von `icon={sd path}` (bevorzugte Methode) genutzt werden, die auf ein BMP verweisen sollte.
