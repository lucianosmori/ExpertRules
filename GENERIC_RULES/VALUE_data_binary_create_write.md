# REGISTRY VALUE DATA BINARY ASSIGNMENT PROTECTION RULE

## Description
This rule prevents from creating a new **binary** registry value with the data **fe340ead** or assign such data to an already existing one in the hive **HKEY_LOCAL_MACHINE\\SOFTWARE\\TestRegvalData\\** using any program.

## Rule TCL
```
Rule {
    Process {
        Include OBJECT_NAME { -v ** }
    }
    Target {
        Match VALUE {
            Include OBJECT_NAME {
               -v "HKLM\\Software\\TestRegvalData\\**"
            }
            Include REGVAL_DATA -type BINARY {
               -v fe340ead
            }
            Include -access "CREATE WRITE"
        }
    }
}
```

## Trigger
1. Add and enforce the rule to the exploit prevention policy.
1. Open Windows CMD with Admin rights.
1. Run the following command:<br>
`reg add HKEY_LOCAL_MACHINE\SOFTWARE\TestRegvalData /v testbin /t REG_BINARY /d fe340ead`

## Notes
