# Optional LF-only line-ending policy

The template is neutral by default: it does not force a line-ending policy
on every project created from it. Some projects need CRLF for specific
files, some teams have established editor settings, and public template
users should not get a surprise mechanical rewrite.

If you want an LF-only repository, opt in after creating the derived
project:

```bash
python _template/apply-lf-policy.py
```

This adds:

```gitattributes
* text=auto eol=lf

*.gif binary
*.gz binary
*.ico binary
*.jpeg binary
*.jpg binary
*.pdf binary
*.png binary
*.webp binary
```

and:

```ini
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
```

## What the files do

`.gitattributes` is the repository guard. `text=auto` lets Git detect
text files; `eol=lf` checks those files out with LF line endings. The
binary patterns keep common binary formats out of text normalization.

`.editorconfig` is the editor hint. Supporting editors should create and
save text files as UTF-8 with LF endings. It does not rewrite existing
files by itself, but an editor may apply it when saving a file.

## Git config check

The script reports relevant Git settings and warns about risky values:

* `core.autocrlf=true` can create CRLF working-tree files in repositories
  without a `.gitattributes` guard.
* `core.eol=crlf` conflicts with an LF-only repo policy.
* `core.autocrlf=input`, `core.autocrlf=false`, or unset are usually fine
  when `.gitattributes` pins the repository policy.

The script only reports Git config. It never changes local or global Git
configuration.

## Existing projects

For an existing repository, run the cleanup as a dedicated mechanical
change:

```bash
python _template/apply-lf-policy.py --dry-run
python _template/apply-lf-policy.py
git status --short
git diff --stat
# run the project's tests/build
git commit -m "chore: normalize text files to LF"
```

Review risky files before committing, especially tracked data stores,
fixtures, generated files, vendored code, `.bat` / `.cmd`, archives,
databases, and unknown binary formats.
