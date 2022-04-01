# README

## Mayukai Theme

<div align="center">

[![vscode](https://img.shields.io/badge/VS%20Code-Theme-success?style=for-the-badge&labelColor=ffa323&color=ff6337)](https://github.com/GulajavaMinistudio/Mayukai-Theme) [![indonesiamessage](https://img.shields.io/badge/FROM-INDONESIA%20WITH%20LOVE-red?style=for-the-badge&labelColor=f66767&color=f0134d)](https://github.com/GulajavaMinistudio/Mayukai-Theme)

![heroPreview](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/drawing_mayukai_heros_resize.png)

</div>

Mayukai Theme is dark and yellow bluish mirage theme with bright colors for easy readibility syntax. This theme is inspired from mixed color swatch in Ayu Theme, Material Theme, Monokai, Andromeda, and Gruvbox Darktooth Original Colors. These color are adjusted in Mayukai theme so it suitable for all day long programming work. This theme also included with built-in File Icon Theme called Mayukai Ayu.

## Install in VS Code/VS Codium

Open Visual Studio Code Market Place in your Visual Studio Code or VS Codium text editor, and search Mayukai. Hit install button, and after finishing install, go to `Preferences > Color Theme > Mayukai Dark or Mayukai Mirage`. If you want to use built-in File Icon Theme, go to `Preferences > File Icon Theme > Mayukai Ayu`.

## List of Color Scheme

This Mayukai Theme includes some color scheme for syntax coloring. There are :

- Mayukai Mirage.
- Mayukai Semantic Mirage (specially designed for VS Code Semantic Highlighting feature).
- Mayukai Dark.
- Mayukai Mirage Gruvbox Darktooth.
- Mayukai Mono.
- Mayukai Alucard.
- Mayukai Sunset.
- Mayukai Reversal.
- Mayukai Midnight.

---

## Preview and Screenshot

Some demo for syntax highlighting in JavaScript, CSS, HTML, and JSON file. The recommended font for use with this theme is [Iosevka Font](https://github.com/be5invis/Iosevka) or using our custom build font named [Iosevka Mayukai](https://github.com/Iosevka-Mayukai/Iosevka-Mayukai).

### Mayukai Mirage JavaScript Syntax

![Screenshot1](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo1.png)

### Mayukai Mirage HTML Syntax

![Screenshot2](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo2.png)

### Mayukai Mirage CSS SCSS Syntax

![Screenshot3](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo3.png)

### Mayukai Mirage JSON Syntax

![Screenshot4](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo4.png)

### Mayukai Dark

![Screenshot5](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo6.png)

### Mayukai Gruvbox Darktooth

![Screenshot6](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo5.png)

### Mayukai Mono

![Screenshot7](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo7.png)

### Mayukai Alucard

![Screenshot8](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo8.png)

### Mayukai Sunset

![Screenshot9](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo9.png)

### Mayukai Reversal

![Screenshot10](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo10.png)

### Mayukai Midnight

![Screenshot10](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/master/scrdemo11.png)


## Known Issues

VS Code 1.50 and newer versions, bring new feature called Semantic Highlighting. Unfortunately, this feature make VS Code theme and syntax highlighting broken and unusable. You can disable this feature in VS Code Settings.

Put this line in your VS Code **_settings.json_** file.

```sh
"editor.semanticHighlighting.enabled": false
```

```sh
"editor.semanticTokenColorCustomizations": { "enabled": false }
```

Related Issue :

[https://github.com/microsoft/vscode/issues/92308](https://code.visualstudio.com/docs/getstarted/themes#_semantic-highlighting)

Reference :

[https://code.visualstudio.com/docs/getstarted/themes#\_semantic-highlighting](https://code.visualstudio.com/docs/getstarted/themes#_semantic-highlighting)

Reference :

[https://github.com/microsoft/vscode/wiki/Semantic-Highlighting-Overview](https://github.com/microsoft/vscode/wiki/Semantic-Highlighting-Overview)

Or search in your VS Code Settings with "semantic" keyword. And disable by selecting **false option** from **_Editor > Semantic Highlighting: Enabled_** dropdown setting.

![Semantic Setting](https://raw.githubusercontent.com/GulajavaMinistudio/Mayukai-Theme/semantic/bugs_semantic1.png)

## Mayukai Theme for Semantic Highlighting VS Code

If you still want use Semantic Highlighting in VS Code 1.45.x and newer versions. You can use Mayukai Theme that specially designed for Semantic Highlighting. Just select **Mayukai Semantic Mirage** Theme in Color Theme Setting in your VS Code.

## Miscellaneous

Mayukai theme also available in [Hyper Terminal](https://hyper.is/) . You can download and install Mayukai Hyper Terminal Theme in [this link](https://github.com/cevr/hyper-mayukai).

Mayukai Theme work fine with other syntax highlighting extension, such as [Babel JavaScript](https://marketplace.visualstudio.com/items?itemName=mgmcdermott.vscode-language-babel) by Michael McDermott. But I recommended you to disable that extension if you find any problem with syntax coloring consistency in Mayukai Theme.

Mayukai Terminal Theme also available for Linux System, with .Xresources configuration. This configuration and how to install available in this repository [Mayukai Terminal Theme](https://github.com/irrellia/mayukai-terminal-themes).

---

## Development

This theme is using base color swatch from Ayu, with some adjustment for syntax coloring. Template for this theme is generated using Ayu Color Generator from [Ayu Theme](https://github.com/ayu-theme/vscode-ayu). Documentation used for creating this theme in [VS Code Theming API](https://code.visualstudio.com/api/references/theme-color).

---

## Thank you for

Thank you to everyone who create these amazing theme in VS Code that inspires Mayukai Theme, feel free to check and try this out.

- [Ayu Theme](https://github.com/ayu-theme/vscode-ayu) and for [Ayu color](https://github.com/ayu-theme/ayu-colors) swatch.
- [Ayu Icon Theme](https://github.com/ayu-theme/vscode-ayu) for built in icon theme.
- [Material Theme](https://github.com/material-theme/vsc-material-theme)
- [Andromeda Theme](https://github.com/EliverLara/Andromeda)
- [Monokai theme](https://github.com/microsoft/vscode/tree/master/extensions/theme-monokai) that built in on VS Code.
- [Gruvbox Color Scheme](https://github.com/morhetz/gruvbox) by Pavel Pertsev.
- [Darktooth Color Scheme](https://github.com/emacsfodder/emacs-theme-darktooth) .
- [Dracula Color Scheme](https://github.com/dracula/dracula-theme) .

---

### Issue and Bug Report

We know creating syntax theme that run on every syntax in every programming language is hard, and we know that Mayukai theme is far from perfect. This theme will be updated regulary for coloring adjustment. And if you find any issue or bug in this theme, feel free to make an Issue in this repository.

**Enjoy!**
