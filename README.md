# Pangolino language data

Language data for Pangolino, an on-device grammar and spell checker for English and German. The
files are compiled from LanguageTool's rules and word lists and from the dictionaries listed
below. This repository is served with GitHub Pages at `https://limosa-labs.github.io/pangolino-data/`.

Pangolino's release workflow adds each version. Nobody edits a published version.

## Layout

```
<data version>/manifest.json         integrity manifest for that version
<data version>/en/<artifact>.gz      English artifacts
<data version>/de/<artifact>.gz      German artifacts
NOTICE                               attributions for every data source
licenses/                            licence texts and the dictionaries' own terms
```

A data version looks like `v6.8-s5-0123456789ab`: the LanguageTool version, the artifact schema
version, and the first 12 hex digits of a SHA-256 over the files' paths and hashes. An identical
rebuild gives the same version, so a version folder never changes once it is published.

`manifest.json` lists every file with its `path`, the SHA-256 and size of the `.gz` file, the raw
size and the load group. Download `<data version>/<path>` and check the SHA-256 before use. The
files are plain gzip streams, served as `application/gzip` without `Content-Encoding`.

## Licences

The artifacts are derived works of the sources below and are distributed under their terms.
Details and copyright notices are in [`NOTICE`](NOTICE).

| Source | Licence | Text |
|---|---|---|
| LanguageTool 6.8 rules, word lists, disambiguation and segmentation data | LGPL 2.1 or later | [`licenses/LGPL-2.1.txt`](licenses/LGPL-2.1.txt) |
| English POS and spelling dictionaries (`english-pos-dict` 0.6) | LGPL 2.1; the spelling lists come from SCOWL, the POS data from Moby, WordNet, AGID and 12dicts, under their own notices | [`licenses/LGPL-2.1.txt`](licenses/LGPL-2.1.txt), [`licenses/dictionaries/`](licenses/dictionaries/) |
| German POS dictionary (`german-pos-dict` 1.2.4, based on Morphy) | CC BY-SA 4.0 | [`licenses/CC-BY-SA-4.0.txt`](licenses/CC-BY-SA-4.0.txt) |
| German Hunspell dictionary `de_DE` (igerman98 / frami, with Jan Schreiber's public-domain word list) | GPL version 2 or 3 | [`licenses/GPL-2.0.txt`](licenses/GPL-2.0.txt), [`licenses/GPL-3.0.txt`](licenses/GPL-3.0.txt) |
| jWordSplitter 4.7 word list and exception splits | Apache 2.0 | [`licenses/Apache-2.0.txt`](licenses/Apache-2.0.txt) |
| Apache OpenNLP 1.5 English tokenizer, POS and chunker models | Apache 2.0 | [`licenses/Apache-2.0.txt`](licenses/Apache-2.0.txt) |

## Sources

Every version up to the next LanguageTool upgrade is built from exactly these inputs. Each
version's `manifest.json` names its LanguageTool version in `ltVersion`.

- **LanguageTool v6.8:** <https://github.com/languagetool-org/languagetool/tree/v6.8>, commit
  [`e807fcde6a6506191e1470744d2345da28c26be6`](https://github.com/languagetool-org/languagetool/tree/e807fcde6a6506191e1470744d2345da28c26be6).
  The build reads `languagetool-core/src/main/resources` and the `en` and `de` modules under
  `languagetool-language-modules/`.
- **Dictionaries and models,** the Maven Central artifacts LanguageTool 6.8 depends on:

  | Artifact | SHA-256 of the jar | Project |
  |---|---|---|
  | [`org.languagetool:english-pos-dict:0.6`](https://repo1.maven.org/maven2/org/languagetool/english-pos-dict/0.6/english-pos-dict-0.6.jar) | `2a3e96b49854e5275f8eb7a1bb5b3b85b82f687fed272f3043882ccc0b1634b1` | <https://github.com/languagetool-org/english-pos-dict> |
  | [`de.danielnaber:german-pos-dict:1.2.4`](https://repo1.maven.org/maven2/de/danielnaber/german-pos-dict/1.2.4/german-pos-dict-1.2.4.jar) | `56f0b00adb704cbc1e86776b45f6890efe90685ab370a34b5b299593cdcaae22` | <https://github.com/languagetool-org/german-pos-dict> |
  | [`de.danielnaber:jwordsplitter:4.7`](https://repo1.maven.org/maven2/de/danielnaber/jwordsplitter/4.7/jwordsplitter-4.7.jar) | `0435e604abe8b4a0b27f568db9349fbe0546df286bbe62f667c9fd9663df71b2` | <https://github.com/danielnaber/jwordsplitter/tree/v4.7> |
  | [`edu.washington.cs.knowitall:opennlp-tokenize-models:1.5`](https://repo1.maven.org/maven2/edu/washington/cs/knowitall/opennlp-tokenize-models/1.5/opennlp-tokenize-models-1.5.jar) | `1c10141d547b9ae1de1238d5a9ec69db043289cd6f8caf0d7d2f14bbfcda9502` | <http://opennlp.sourceforge.net/models-1.5/> |
  | [`edu.washington.cs.knowitall:opennlp-postag-models:1.5`](https://repo1.maven.org/maven2/edu/washington/cs/knowitall/opennlp-postag-models/1.5/opennlp-postag-models-1.5.jar) | `4d58462b891dbe478a8a68c8a93749af5bedd874af1974596a72f5667fffc8c9` | <http://opennlp.sourceforge.net/models-1.5/> |
  | [`edu.washington.cs.knowitall:opennlp-chunk-models:1.5`](https://repo1.maven.org/maven2/edu/washington/cs/knowitall/opennlp-chunk-models/1.5/opennlp-chunk-models-1.5.jar) | `e7090de37093d2b91a0136f9e1e9cf60567bc27f72781cfdd083d86e342d7cb0` | <http://opennlp.sourceforge.net/models-1.5/> |

- **German Hunspell `de_DE`:** shipped inside LanguageTool v6.8 at
  [`languagetool-language-modules/de/src/main/resources/org/languagetool/resource/de/hunspell/`](https://github.com/languagetool-org/languagetool/tree/v6.8/languagetool-language-modules/de/src/main/resources/org/languagetool/resource/de/hunspell)
  (`de_DE.aff`, `de_DE.dic`, `de_DE.dict`). Upstream: <https://www.j3e.de/ispell/igerman98/> and
  <https://extensions.libreoffice.org/extensions/german-de-de-frami-dictionaries>.
- **English spelling lists (SCOWL):** <http://wordlist.aspell.net/>. The README files LanguageTool
  ships with them are in [`licenses/dictionaries/`](licenses/dictionaries/).

Pangolino's build tools compile these inputs into the artifacts. The commit message of each
version names the Pangolino commit that built it.
