# cymraeg-english-open-argos-models

Cymraeg-English Translation models for OpenArgos and LibreTranslate (uses https://github.com/Helsinki-NLP/OPUS-MT-train models converted for use with argos)

## Conversion process

As per <https://github.com/LibreTranslate/Locomotive?tab=readme-ov-file#convert-helsinki-nlp-opus-mt-models> but with the following additional python dependencies:

```
stanza = "1.6.0"
iso639 = "^0.1.4"
ctranslate2 = "^4.7.1"
```

Oh, and a small change in `opus_mt_convert.py`:

```diff
diff --git a/opus_mt_convert.py b/opus_mt_convert.py
index 520b71d..bbeaf31 100644
--- a/opus_mt_convert.py
+++ b/opus_mt_convert.py
@@ -215,7 +215,7 @@ if not os.path.isdir(os.path.join(stanza_dir, stanza_lang_code)):
     while True:
         try:
             os.makedirs(stanza_dir, exist_ok=True)
-            stanza.download(stanza_lang_code, dir=stanza_dir, processors="tokenize")
+            stanza.download(stanza_lang_code, model_dir=stanza_dir, processors="tokenize")
             break
         except Exception as e:
             print(f'Cannot download stanza model: {str(e)}')
```
