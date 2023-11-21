# RunFinger
RunFinger will scan the environment for window machines.  This command will build a targets file that can be used with crackmapexec.

```
/usr/share/responder/tools/RunFinger.py -i <*.*.*.*/**> | grep "Signing:'False'"|cut -d "'" -f 2 >><filename>.txt
```
