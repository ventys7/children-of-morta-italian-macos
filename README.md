# Children of Morta – Italian Translation for macOS 🇮🇹

Porting per macOS della traduzione italiana community di **Children of Morta**.

Un piccolo progetto nato per un motivo molto semplice: volevo giocare a Children of Morta in italiano sul mio Mac, ma la traduzione della community disponibile online non funzionava sulla versione macOS.

Invece di rinunciare, ho provato a capire cosa non andasse e ad adattarla. Questo repository raccoglie il risultato di quel lavoro.

## 🙏 Crediti

Un ringraziamento speciale a **banz99, SLegend29 e AB_Jab** per aver realizzato la traduzione italiana originale.

Senza il loro lavoro questo progetto non sarebbe stato possibile.

La traduzione originale è disponibile qui:

[Children of Morta – Traduzione italiana su Steam Community](https://steamcommunity.com/sharedfiles/filedetails/?id=2363914586)

---

## 🎮 Stato del progetto

**Il porting funziona!**

Ho installato e testato la traduzione sulla versione macOS GOG di Children of Morta.

Il gioco si avvia, i testi vengono visualizzati correttamente e anche i caratteri accentati funzionano.

Per il momento ho testato personalmente il **prologo**, che si è svolto senza crash, menu vuoti o problemi evidenti.

Non ho ancora iniziato una partita vera e propria e, di conseguenza, non posso garantire che ogni singolo testo, evento o situazione del gioco sia stato verificato.

Il progetto rimane aperto a eventuali correzioni e miglioramenti. Man mano che continuerò a giocare, aggiornerò il porting e questa documentazione nel caso emergano problemi.

Insomma, il vero test comincia adesso. Vediamo anche se riuscirò a finirlo! 😂

## 📖 Da dove nasce tutto

La traduzione italiana di Children of Morta esiste già ed è un ottimo lavoro della community.

È stata realizzata da **banz99, SLegend29 e AB_Jab** e comprende oltre 60.000 parole, tra dialoghi, menu, oggetti, descrizioni e contenuti aggiuntivi, DLC compresi.

Il problema è che la patch originale era destinata a Windows. Installandola direttamente sulla versione Mac si potevano verificare crash, menu vuoti e altri problemi.

Non aveva molto senso rifare da zero una traduzione già esistente, quindi ho provato a capire cosa impedisse alla patch di funzionare su macOS.

La causa era nella struttura degli asset Unity: i file della patch erano costruiti per Windows, mentre quelli del gioco Mac erano destinati a macOS.

Da lì è iniziato il lavoro di adattamento.

## 🔧 Cosa è stato fatto

### 1. Adattamento dei testi

Il bundle `core` contiene i testi utilizzati dal gioco.

L'analisi ha mostrato che la patch italiana e la versione Mac contenevano esattamente gli stessi 58 TextAsset, con gli stessi identificativi e la stessa struttura.

Su questi 58 asset, 23 presentavano modifiche nella patch italiana.

I contenuti tradotti sono stati trasferiti nei rispettivi asset della versione Mac, mantenendo gli identificativi originali e la piattaforma di destinazione macOS.

Una particolarità della patch originale: i testi italiani sono inseriti principalmente nello slot linguistico spagnolo (`ES`). Per questo motivo, una volta installata, è necessario selezionare **Español** nelle impostazioni del gioco per visualizzare l'italiano.

### 2. Correzione del font e degli accenti

Dopo aver adattato i testi, il gioco funzionava correttamente, ma gran parte degli accenti italiani non veniva visualizzata.

Il problema era legato al font `Fairfax SDF`.

La patch originale conteneva una versione modificata del font e del relativo atlante grafico, necessari per visualizzare correttamente alcuni caratteri italiani.

Sono state quindi recuperate e trasferite soltanto le due risorse interessate:

- `Fairfax SDF` – MonoBehaviour, Path ID 239.
- `Fairfax SDF Atlas` – Texture2D, Path ID 40.

In questo modo è stato possibile recuperare i glifi mancanti, tra cui `È`, `ì` e `ò`, insieme alle relative informazioni grafiche.

I 30 shader che differivano tra le versioni Windows e macOS sono rimasti quelli originali del gioco Mac.

Anche il nuovo `resources.assets` conserva la piattaforma macOS.

## ✅ Risultato

Il porting è stato verificato tecnicamente e provato direttamente nel gioco.

| Elemento | Risultato |
|---|---|
| Traduzione italiana | Funzionante |
| Menu e interfaccia | Testati nel prologo |
| Dialoghi e sottotitoli | Testati nel prologo |
| Descrizioni e oggetti | Testati nel prologo |
| Caratteri accentati | Corretti |
| Compatibilità AssetBundle macOS | Verificata |
| Shader originali Mac | Conservati |
| Crash durante il prologo | Nessuno riscontrato |

La traduzione non utilizza servizi AI, API esterne o sistemi di traduzione in tempo reale.

I testi italiani provengono direttamente dal lavoro originale della community.

## 💻 Compatibilità

Ambiente utilizzato per realizzare e testare il porting:

| Componente | Versione |
|---|---|
| Gioco | Children of Morta – GOG |
| Patch italiana originale | GOG 1.2.74 |
| Sistema operativo | macOS |
| Architettura | Intel x86_64 |
| Unity | 2019.2.15f1 |

La compatibilità è stata verificata sulla versione GOG per Mac Intel.

Non sono ancora state testate:
- Versione Steam.
- Mac con Apple Silicon.
- Altre versioni o aggiornamenti del gioco.
- L'intera campagna e tutti i DLC.

---

# 📥 Installazione

La procedura è stata realizzata e testata su macOS Intel.

Per applicare la traduzione servono:
- Una copia GOG di Children of Morta per macOS.
- La patch italiana originale della community.
- Python 3.
- Una connessione Internet per scaricare le dipendenze Python.

Non è necessario installare BepInEx o UnityGameTranslator.

## 1. Scaricare la traduzione originale

La patch italiana originale è disponibile qui:

**[Google Drive – Children of Morta Italian Translation](https://drive.google.com/drive/folders/1OqNdRXgzNAENQjm9zx_X4K6t_0TnHJaV)**

Scaricare il file:

`GoG CoM_Italian 1.2.74.zip`

Salvare il file nella cartella `Downloads`, senza estrarlo.

La traduzione originale è stata realizzata da banz99, SLegend29 e AB_Jab. Questo progetto non ne rivendica la paternità.

## 2. Preparare Python e le dipendenze

Aprire il Terminale e verificare che Python 3 sia disponibile:

```bash
python3 --version
```

Creare un ambiente Python dedicato:

```bash
python3 -m venv "$HOME/Downloads/UnityPy-Inspect"

"$HOME/Downloads/UnityPy-Inspect/bin/python" -m pip install --upgrade pip

"$HOME/Downloads/UnityPy-Inspect/bin/python" -m pip install UnityPy Pillow typetreegeneratorapi
```

L'installazione delle dipendenze potrebbe richiedere qualche minuto.

## 3. Verificare i percorsi

La procedura utilizza questi percorsi:

**Gioco:**

`/Applications/Children of Morta.app`

**Patch italiana:**

`~/Downloads/GoG CoM_Italian 1.2.74.zip`

Se il gioco si trova in una cartella differente, sarà necessario modificare il percorso nei comandi successivi.

## 4. Adattare il bundle dei testi (core)

Il primo passaggio consiste nel trasferire i 23 TextAsset modificati dalla patch originale al bundle macOS.

Vengono mantenuti gli identificativi originali e la piattaforma di destinazione del gioco Mac.

Aprire il Terminale e incollare:

```bash
DIR="$HOME/Downloads"
DATA="/Applications/Children of Morta.app/Contents/Resources/Data"
PY="$HOME/Downloads/UnityPy-Inspect/bin/python"

"$PY" - "$DIR" "$DATA" <<'PY'
import sys, os, zipfile, hashlib
import UnityPy

folder, data = sys.argv[1:3]

archive = os.path.join(folder, "GoG CoM_Italian 1.2.74.zip")
original = os.path.join(data, "StreamingAssets/AssetBundles/core")
output = os.path.join(folder, "CoM-core-Italian-Mac-test")
member = "StreamingAssets/AssetBundles/core"

print("Caricamento patch italiana...")
with zipfile.ZipFile(archive) as z:
    patch_env = UnityPy.load(z.read(member))

print("Caricamento bundle Mac originale...")
mac_env = UnityPy.load(original)

patch_objs = {
    obj.path_id: obj
    for obj in patch_env.objects
    if obj.type.name == "TextAsset"
}

mac_objs = {
    obj.path_id: obj
    for obj in mac_env.objects
    if obj.type.name == "TextAsset"
}

if len(patch_objs) != 58 or len(mac_objs) != 58:
    raise SystemExit("STOP: numero di TextAsset inatteso.")

if set(patch_objs) != set(mac_objs):
    raise SystemExit("STOP: Path ID non corrispondenti.")

changed = []

for pid in sorted(patch_objs):
    p_obj = patch_objs[pid]
    m_obj = mac_objs[pid]

    p_data = p_obj.parse_as_object()
    m_data = m_obj.parse_as_object()

    if p_data.m_Name != m_data.m_Name:
        raise SystemExit("STOP: nome asset differente.")

    if p_data.m_Script != m_data.m_Script:
        changed.append((pid, p_obj, m_obj, p_data.m_Name))

if len(changed) != 23:
    raise SystemExit(
        f"STOP: attese 23 modifiche, trovate {len(changed)}."
    )

platforms = {asset.target_platform for asset in mac_env.assets}

if platforms != {2}:
    raise SystemExit(f"STOP: piattaforma Mac inattesa: {platforms}")

print("Asset da aggiornare:", len(changed))

for pid, p_obj, m_obj, name in changed:
    translated = p_obj.parse_as_object()
    original_data = m_obj.parse_as_object()

    original_data.m_Script = translated.m_Script
    m_obj.patch(original_data)

    print("Aggiornato:", name)

print("Salvataggio bundle Mac...")

result = mac_env.file.save(packer="original")

with open(output, "wb") as f:
    f.write(result)

print("Verifica del nuovo bundle...")

check = UnityPy.load(output)

check_platforms = {asset.target_platform for asset in check.assets}

if check_platforms != {2}:
    os.remove(output)
    raise SystemExit("ERRORE: piattaforma modificata.")

check_objs = {
    obj.path_id: obj
    for obj in check.objects
    if obj.type.name == "TextAsset"
}

for pid, p_obj, _, name in changed:
    expected = p_obj.parse_as_object().m_Script
    actual = check_objs[pid].parse_as_object().m_Script

    if expected != actual:
        os.remove(output)
        raise SystemExit("ERRORE verifica testo: " + name)

print("Piattaforma conservata:", check_platforms)
print("TextAsset verificati:", len(check_objs))
print("Traduzioni trasferite:", len(changed))
print("Dimensione:", len(result), "bytes")
print("SHA256:", hashlib.sha256(result).hexdigest())
print("File creato:", output)
print("Originali non modificati.")
PY
```

Al termine verrà creato:

`~/Downloads/CoM-core-Italian-Mac-test`

## 5. Adattare il font e il bundle resources.assets

Il secondo passaggio serve a recuperare i caratteri accentati italiani.

La patch originale contiene il font `Fairfax SDF` modificato e la relativa texture. Questi elementi devono essere trasferiti senza importare gli shader della versione Windows.

Viene utilizzato il TypeTree del gioco Mac per leggere correttamente gli oggetti della patch Windows.

Incollare nel Terminale:

```bash
DIR="$HOME/Downloads"
DATA="/Applications/Children of Morta.app/Contents/Resources/Data"
MANAGED="$DATA/Managed"
PY="$HOME/Downloads/UnityPy-Inspect/bin/python"
OUT="$HOME/Downloads/CoM-resources-Italian-Mac-test"

"$PY" - "$DIR" "$DATA" "$MANAGED" "$OUT" <<'PY'
import sys, os, zipfile
import UnityPy
from UnityPy.helpers.TypeTreeGenerator import TypeTreeGenerator

folder, data, managed, output = sys.argv[1:5]

archive = os.path.join(folder, "GoG CoM_Italian 1.2.74.zip")

gen = TypeTreeGenerator("2019.2.15f1")
gen.load_local_dll_folder(managed)

with zipfile.ZipFile(archive) as z:
    patch_env = UnityPy.load(z.read("resources.assets"))

mac_env = UnityPy.load(os.path.join(data, "resources.assets"))
mac_env.typetree_generator = gen

def find(env, path_id, expected_type):
    obj = next(
        (
            o for o in env.objects
            if o.path_id == path_id
            and o.type.name == expected_type
        ),
        None
    )

    if obj is None:
        raise RuntimeError(
            f"Oggetto non trovato: {expected_type} ID {path_id}"
        )

    return obj

patch_font = find(patch_env, 239, "MonoBehaviour")
mac_font = find(mac_env, 239, "MonoBehaviour")

patch_tex = find(patch_env, 40, "Texture2D")
mac_tex = find(mac_env, 40, "Texture2D")

print("Creazione degli schemi originali Mac...")

font_node = mac_font._get_typetree_node()
texture_node = mac_tex._get_typetree_node()

font_tree = patch_font.parse_as_dict(node=font_node)
texture_tree = patch_tex.parse_as_dict(node=texture_node)

if font_tree["m_Name"] != "Fairfax SDF":
    raise SystemExit("Nome font inatteso.")

if texture_tree["m_Name"] != "Fairfax SDF Atlas":
    raise SystemExit("Nome texture inatteso.")

required = {0x00C8, 0x00EC, 0x00F2}

patch_chars = {
    item["m_Unicode"]
    for item in font_tree["m_CharacterTable"]
}

if not required.issubset(patch_chars):
    raise SystemExit("Glifi italiani mancanti nella patch.")

print("Glifi italiani verificati.")

print("Trasferimento Fairfax SDF...")
mac_font.patch(font_tree)

print("Trasferimento Fairfax SDF Atlas...")
mac_tex.patch(texture_tree)

platforms = {asset.target_platform for asset in mac_env.assets}

if platforms != {2}:
    raise SystemExit("Piattaforma originale non macOS.")

print("Salvataggio resources.assets...")

result = mac_env.file.save(packer="original")

with open(output, "wb") as f:
    f.write(result)

print("Verifica del nuovo bundle...")

original = UnityPy.load(os.path.join(data, "resources.assets"))
original.typetree_generator = gen

original_font = find(original, 239, "MonoBehaviour")
font_node = original_font._get_typetree_node()

check = UnityPy.load(output)

check_platforms = {asset.target_platform for asset in check.assets}

if check_platforms != {2}:
    os.remove(output)
    raise SystemExit("Piattaforma errata.")

new_font = find(check, 239, "MonoBehaviour").parse_as_dict(
    node=font_node
)

new_chars = {
    item["m_Unicode"]
    for item in new_font["m_CharacterTable"]
}

if not required.issubset(new_chars):
    os.remove(output)
    raise SystemExit("Verifica glifi fallita.")

for code, char in [
    (0x00C8, "È"),
    (0x00EC, "ì"),
    (0x00F2, "ò")
]:
    print(char, "PRESENTE" if code in new_chars else "ASSENTE")

if not required.issubset(new_chars):
    os.remove(output)
    raise SystemExit("Caratteri italiani non verificati.")

new_tex = find(check, 40, "Texture2D")
patch_tex = find(patch_env, 40, "Texture2D")

from PIL import ImageChops

image_patch = patch_tex.read().image.convert("RGBA")
image_new = new_tex.read().image.convert("RGBA")

if ImageChops.difference(image_patch, image_new).getbbox():
    os.remove(output)
    raise SystemExit("Atlante grafico differente.")

print("Atlante grafico verificato.")
print("Target Platform:", check_platforms)
print("Caratteri font:", len(new_chars))
print("Dimensione:", len(result), "bytes")
print("File creato:", output)
print("Originali non modificati.")
PY
```

Al termine verrà creato:

`~/Downloads/CoM-resources-Italian-Mac-test`

## 6. Preparare i file per l'installazione

Creare la cartella contenente i due file adattati:

```bash
mkdir -p "$HOME/Downloads/CoM-Italian-Mac"

cp "$HOME/Downloads/CoM-core-Italian-Mac-test" \
"$HOME/Downloads/CoM-Italian-Mac/core"

cp "$HOME/Downloads/CoM-resources-Italian-Mac-test" \
"$HOME/Downloads/CoM-Italian-Mac/resources.assets"

echo "File preparati."
ls -lh "$HOME/Downloads/CoM-Italian-Mac/"
```

La cartella deve contenere:

```text
CoM-Italian-Mac/
├── core
└── resources.assets
```

## 7. Installare la traduzione

Chiudere completamente Children of Morta.

Verificare che il gioco si trovi in `/Applications/Children of Morta.app`.

Incollare nel Terminale:

```bash
set -e

APP="/Applications/Children of Morta.app/Contents/Resources/Data"
PATCH="$HOME/Downloads/CoM-Italian-Mac"

CORE="$APP/StreamingAssets/AssetBundles/core"
RESOURCES="$APP/resources.assets"

if [ ! -f "$PATCH/core" ] || [ ! -f "$PATCH/resources.assets" ]; then
  echo "File della traduzione mancanti."
  exit 1
fi

STAMP=$(date +%Y%m%d-%H%M%S)
BACKUP="$HOME/Downloads/CoM-Italian-Mac-backup-$STAMP"

mkdir -p "$BACKUP"

cp -p "$CORE" "$BACKUP/core"
cp -p "$RESOURCES" "$BACKUP/resources.assets"

printf '%s\n' "$BACKUP" > "$HOME/Downloads/CoM-Italian-Mac-backup-last.txt"

CORE_UID=$(stat -f '%u' "$CORE")
CORE_GID=$(stat -f '%g' "$CORE")
CORE_MODE=$(stat -f '%Lp' "$CORE")

RES_UID=$(stat -f '%u' "$RESOURCES")
RES_GID=$(stat -f '%g' "$RESOURCES")
RES_MODE=$(stat -f '%Lp' "$RESOURCES")

sudo -v

sudo cp "$PATCH/core" "$CORE"
sudo cp "$PATCH/resources.assets" "$RESOURCES"

sudo chown "$CORE_UID:$CORE_GID" "$CORE"
sudo chmod "$CORE_MODE" "$CORE"

sudo chown "$RES_UID:$RES_GID" "$RESOURCES"
sudo chmod "$RES_MODE" "$RESOURCES"

if ! cmp -s "$PATCH/core" "$CORE" || ! cmp -s "$PATCH/resources.assets" "$RESOURCES"; then
  echo "Errore durante l'installazione."

  sudo cp -p "$BACKUP/core" "$CORE"
  sudo cp -p "$BACKUP/resources.assets" "$RESOURCES"

  exit 1
fi

echo ""
echo "Traduzione installata correttamente!"
echo "Backup originale:"
echo "$BACKUP"
```

## 8. Avviare il gioco

Aprire Children of Morta normalmente dal Finder.

Nelle impostazioni della lingua selezionare:

**Español**

La traduzione italiana utilizza lo slot linguistico spagnolo della patch originale.

## 9. Ripristinare i file originali

Per tornare alla versione originale del gioco, chiuderlo e incollare:

```bash
set -e

APP="/Applications/Children of Morta.app/Contents/Resources/Data"
BACKUP_FILE="$HOME/Downloads/CoM-Italian-Mac-backup-last.txt"

if [ ! -f "$BACKUP_FILE" ]; then
  echo "Backup non trovato."
  exit 1
fi

BACKUP=$(cat "$BACKUP_FILE")

if [ ! -f "$BACKUP/core" ] || [ ! -f "$BACKUP/resources.assets" ]; then
  echo "File di backup mancanti."
  exit 1
fi

sudo cp -p "$BACKUP/core" "$APP/StreamingAssets/AssetBundles/core"
sudo cp -p "$BACKUP/resources.assets" "$APP/resources.assets"

echo "Versione originale ripristinata."
```

---

## 🛠️ Strumenti utilizzati

- [UnityPy](https://github.com/K0lb3/UnityPy) – Lettura, modifica e ricostruzione degli asset Unity.
- [Python](https://www.python.org/) – Analisi e trasferimento dei contenuti.
- [Pillow](https://python-pillow.org/) – Analisi e confronto delle texture.

## ⚖️ Copyright e distribuzione

Questo è un progetto amatoriale e non ufficiale, realizzato per adattare una traduzione community a una versione del gioco non supportata dalla patch originale.

Children of Morta è sviluppato da Dead Mage e pubblicato da 11 bit studios. Tutti i diritti relativi al gioco, ai suoi asset e ai marchi appartengono ai rispettivi proprietari.

La traduzione italiana originale appartiene ai suoi autori.

Questo progetto non è affiliato, approvato o supportato dagli sviluppatori o dai publisher di Children of Morta.

Non vengono distribuiti gli asset originali del gioco né i file proprietari della traduzione. Per utilizzare il porting è necessario possedere una copia legittima del gioco e procurarsi separatamente la traduzione originale.

---

*Made with a little patience, some Python and a lot of trial and error on macOS.* ❤️
