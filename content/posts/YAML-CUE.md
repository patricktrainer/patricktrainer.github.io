
---
    title: YAML-CUE
    date: 2021-01-01    
    draft: true
    tags: []
---
# YAML-CUE# YAML | CUE
Created: October 26, 2022 1:04 AM
URL: https://cuelang.org/docs/integrations/yaml/
# YAML
## Intro
Unlike with JSON, CUE is not a superset of YAML.
## Command line tool
### Validate YAML files
The `vet` command of the `cue` command line tool can validate YAML files using a CUE schema.
```
$ cue vet ranges.yaml check.cue
max: invalid value 5 (out of bound >10):
./check.cue:2:16
./ranges.yaml:5:7
```
### Import YAML
The `import` command of the `cue` command line tool can convert YAML files into CUE.
## YAML in CUE
The `encoding/yaml` builtin package provides various builtins to parse, generate, or validate YAML from within CUE.
#Phrases: {
phrases: [string]: #Phrase
#Phrase: {
lang: #LanguageTag
text: !=""
attribution?
phrases: yaml.Validate(#Phrases)
phrases: """
phrases:
# A quote from Mark Twain.
```
$ cue vet dim.cue
phrases: error in call to encoding/yaml.Validate: conflicting values false and
LanguageTag (mismatched types bool and string):
./dim.cue:18:10
```
### Create
The builtin `encoding/yaml.Marshal` generates YAML from within CUE.
