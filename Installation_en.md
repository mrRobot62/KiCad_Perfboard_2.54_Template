# Installing BK_Perfboard_2.54

This guide explains how to install the `BK_Perfboard_2.54` project
template in KiCad 10 on macOS, Windows, and Linux.

## Requirements

-   KiCad 10.x
-   The complete `BK_Perfboard_2.54` template directory
-   Basic KiCad project handling knowledge

## Important: Use the KiCad User Template Directory

KiCad separates system templates from user templates.

`BK_Perfboard_2.54` should be installed in the directory configured by
KiCad as:

`KICAD_USER_TEMPLATE_DIR`

The safest method on every operating system is to check this path
directly in KiCad:

1.  Start KiCad.
2.  Open **Preferences → Configure Paths...**
3.  Find `KICAD_USER_TEMPLATE_DIR`.
4.  Note the directory shown in the **Path** column.
5.  Copy the complete `BK_Perfboard_2.54` directory into that location.

Do not install the template into KiCad's system-template directory.
System templates belong to the KiCad installation and may be replaced by
software updates.

## Required Directory Structure

After installation, the user-template directory should contain the
complete template folder:

``` text
<KICAD_USER_TEMPLATE_DIR>/
└── BK_Perfboard_2.54/
    ├── assets/
    ├── docs/
    ├── footprints/
    ├── meta/
    │   └── info.html
    ├── symbols/
    ├── README.md
    ├── CHANGELOG.md
    ├── BK_Perfboard_2.54.kicad_pcb
    ├── BK_Perfboard_2.54.kicad_pro
    └── BK_Perfboard_2.54.kicad_sch
```

The `meta/info.html` file is required for the template to appear
correctly in KiCad's template selector.

## macOS

### 1. Find the configured template directory

In KiCad:

**Preferences → Configure Paths...**

Check the value of:

``` text
KICAD_USER_TEMPLATE_DIR
```

A typical KiCad 10 setup may use:

``` text
~/Documents/KiCad/10.0/template
```

Do not assume this path is identical on every Mac. The value shown by
KiCad is authoritative.

### 2. Copy the template

Using Finder, copy:

``` text
BK_Perfboard_2.54
```

into the directory shown by `KICAD_USER_TEMPLATE_DIR`.

Or from Terminal, if your configured path is the typical path shown
above:

``` bash
mkdir -p ~/Documents/KiCad/10.0/template
cp -R BK_Perfboard_2.54 ~/Documents/KiCad/10.0/template/
```

After copying, the template should be located at:

``` text
~/Documents/KiCad/10.0/template/BK_Perfboard_2.54
```

## Windows

### 1. Find the configured template directory

In KiCad:

**Preferences → Configure Paths...**

Check:

``` text
KICAD_USER_TEMPLATE_DIR
```

Depending on the installation and user configuration, the directory may
be located under the user's Documents folder or another custom location.

Use the path displayed by KiCad rather than relying on a fixed Windows
path.

### 2. Copy the template

Using File Explorer:

1.  Open the directory shown for `KICAD_USER_TEMPLATE_DIR`.
2.  Copy the complete `BK_Perfboard_2.54` folder into it.

The resulting structure must be:

``` text
<KICAD_USER_TEMPLATE_DIR>\BK_Perfboard_2.54\
```

PowerShell can also be used. Replace `<template-path>` with the path
shown by KiCad:

``` powershell
New-Item -ItemType Directory -Force "<template-path>"
Copy-Item -Recurse ".\BK_Perfboard_2.54" "<template-path>\"
```

## Linux

### 1. Find the configured template directory

In KiCad:

**Preferences → Configure Paths...**

Check:

``` text
KICAD_USER_TEMPLATE_DIR
```

The actual location depends on the Linux distribution, KiCad package,
and user configuration.

Use the path displayed by KiCad as the source of truth.

### 2. Copy the template

Using your file manager, copy the complete:

``` text
BK_Perfboard_2.54
```

directory into the configured user-template directory.

From a terminal:

``` bash
mkdir -p "<template-path>"
cp -R BK_Perfboard_2.54 "<template-path>/"
```

Replace `<template-path>` with the value shown for
`KICAD_USER_TEMPLATE_DIR`.

## Verify the Installation

After copying the template:

1.  Start or restart KiCad if necessary.
2.  Select **File → New Project from Template...**
3.  Open the **User Templates** section.
4.  Select `BK_Perfboard_2.54`.
5.  Confirm that the template information is displayed.
6.  Create a new project from the template.

The new project should open with the prepared perfboard configuration,
including:

-   2.54 mm default grid
-   visual perfboard grid
-   predefined board outline
-   dedicated wire and jumper layers
-   `Bottom Wire (B.Cu)` as the preferred working layer
-   project-local `BK_Perf_SolderPoint` footprint support

## If the Template Does Not Appear

Check the following:

### Verify `KICAD_USER_TEMPLATE_DIR`

Open:

**Preferences → Configure Paths...**

Make sure the template was copied into the directory configured for:

``` text
KICAD_USER_TEMPLATE_DIR
```

### Verify the folder level

Incorrect:

``` text
<KICAD_USER_TEMPLATE_DIR>/
└── BK_Perfboard_2.54/
    └── BK_Perfboard_2.54/
        ├── meta/
        └── ...
```

Correct:

``` text
<KICAD_USER_TEMPLATE_DIR>/
└── BK_Perfboard_2.54/
    ├── meta/
    ├── BK_Perfboard_2.54.kicad_pro
    └── ...
```

### Verify `meta/info.html`

The following file must exist:

``` text
BK_Perfboard_2.54/meta/info.html
```

### Restart KiCad

If the template directory was changed while KiCad was running, restart
KiCad and open the template selector again.

### Use the template selector's folder browser

KiCad can also browse templates from an arbitrary directory. This can be
useful for testing the template before installing it permanently in
`KICAD_USER_TEMPLATE_DIR`.

## Updating the Template

KiCad copies a template when a new project is created.

Existing projects are not automatically synchronized when the installed
template is updated.

To update the template itself:

1.  Replace or update the files in:

    ``` text
    <KICAD_USER_TEMPLATE_DIR>/BK_Perfboard_2.54
    ```

2.  New projects created afterward will use the updated template.

Existing projects remain independent and should only be updated manually
where required.

## Uninstalling

To remove the template, delete:

``` text
<KICAD_USER_TEMPLATE_DIR>/BK_Perfboard_2.54
```

This does not affect projects that were previously created from the
template.

## Further Documentation

For the actual perfboard workflow, see:

-   `docs/Perfboard-Layout_en.md`
-   `docs/Perfboard-Layout_de.md`

The installation guide only covers installing and selecting the KiCad
project template.
