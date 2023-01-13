# 同形异义字符-获得相似的字母，转换成 ASCII，检测可能的语言& UTF 八国集团

> 原文：<https://kalilinuxtutorials.com/homoglyphs-convert-ascii-utf-8-group/>

**同形符号**用于获取相似字母，转换成 ASCII 码，检测可能的语言和 UTF-8 组。也可以说是 python 库，用于获取并转换成 ASCII。 

## **特性**

这是易混淆同形异义词的更聪明的版本:

*   自动检测或手动选择类别(别名来自 ISO 15924)。
*   自动或手动加载只需要在内存中的字母。
*   正在转换为 ASCII。
*   更可配置。
*   更稳定。

**又读[Whatsapp _ Automation:API 集合与运行在 Android 模拟器中的 Whatsapp 交互](https://kalilinuxtutorials.com/whatsapp_automation-android-emulator/)**

## **安装**

```
sudo pip install homoglyphs
```

## **用途**

导入:

```
import homoglyphs as hg
```

## **语言**

```
#detect
hg.Languages.detect('w')
# {'pl', 'da', 'nl', 'fi', 'cz', 'sr', 'pt', 'it', 'en', 'es', 'sk', 'de', 'fr', 'ro'}
hg.Languages.detect('т')
# {'mk', 'ru', 'be', 'bg', 'sr'}
hg.Languages.detect('.')
# set()

# get alphabet for languages
hg.Languages.get_alphabet(['ru'])
# {'в', 'Ё', 'К', 'Т', ..., 'Р', 'З', 'Э'}
```

## **类别**

类别—(来自 ISO 15924 的别名)。

```
#detect
hg.Categories.detect('w')
# 'LATIN'
hg.Categories.detect('т')
# 'CYRILLIC'
hg.Categories.detect('.')
# 'COMMON'

# get alphabet for categories
hg.Categories.get_alphabet(['CYRILLIC'])
# {'ӗ', 'Ԍ', 'Ґ', 'Я', ..., 'Э', 'ԕ', 'ӻ'}
```

## **同形异义字**

明白了吗:

```
# get homoglyphs (latin alphabet initialized by default)
hg.Homoglyphs().get_combinations('q')
# ['q', '𝐪', '𝑞', '𝒒', '𝓆', '𝓺', '𝔮', '𝕢', '𝖖', '𝗊', '𝗾', '𝘲', '𝙦', '𝚚']
```

字母加载:

```
# load alphabet on init by categories
homoglyphs = hg.Homoglyphs(categories=('LATIN', 'COMMON', 'CYRILLIC'))  # alphabet loaded here
homoglyphs.get_combinations('гы')
# ['rы', 'гы', 'ꭇы', 'ꭈы', '𝐫ы', '𝑟ы', '𝒓ы', '𝓇ы', '𝓻ы', '𝔯ы', '𝕣ы', '𝖗ы', '𝗋ы', '𝗿ы', '𝘳ы', '𝙧ы', '𝚛ы']

# load alphabet on init by languages
homoglyphs = hg.Homoglyphs(languages={'ru', 'en'})  # alphabet will be loaded here
homoglyphs.get_combinations('гы')
# ['rы', 'гы']

# manual set alphabet on init      # eng rus
homoglyphs = hg.Homoglyphs(alphabet='abc абс')
homoglyphs.get_combinations('с')
# ['c', 'с']

# load alphabet on demand
homoglyphs = hg.Homoglyphs(languages={'en'}, strategy=hg.STRATEGY_LOAD)
# ^ alphabet will be loaded here for "en" language
homoglyphs.get_combinations('гы')
# ^ alphabet will be loaded here for "ru" language
# ['rы', 'гы']
```

可以任意组合`**categories**`、`**languages**`、`**alphabet**`以及任意策略。

## **将字形转换成 ASCII 字符**

```
homoglyphs = hg.Homoglyphs(languages={'en'}, strategy=hg.STRATEGY_LOAD)

# convert
homoglyphs.to_ascii('тест')
# ['tect']
homoglyphs.to_ascii('ХР123.')  # this is cyrillic "х" and "р"
# ['XP123.', 'XPI23.', 'XPl23.']

# string with chars which can't be converted by default will be ignored
homoglyphs.to_ascii('лол')
# []

# you can set strategy for removing not converted non-ASCII chars from result
homoglyphs = hg.Homoglyphs(
    languages={'en'},
    strategy=hg.STRATEGY_LOAD,
    ascii_strategy=hg.STRATEGY_REMOVE,
)
homoglyphs.to_ascii('лол')
# ['o']
```

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/orsinium/homoglyphs)