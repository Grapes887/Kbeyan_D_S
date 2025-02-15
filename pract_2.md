## Задание 1
```
pip install matplotlib
pip show matplotlib
```
![изображение](https://github.com/user-attachments/assets/2e975c2d-456a-41ea-a648-a849cd825ac5)
## Задание 2
```
git clone https://github.com/expressjs/express.git
cd express
cat package.json
```
![изображение](https://github.com/user-attachments/assets/17f15b5f-96fe-4c67-ab23-a69cd0e92043)

## Задание 3
```
pip install pipdeptree
pipdeptree --packages matplotlib
```
![изображение](https://github.com/user-attachments/assets/6ce40d39-8227-4ec1-b2de-25ee9c77878c)

```
cat package.json
```
![изображение](https://github.com/user-attachments/assets/bf772994-4a86-4edb-948e-7305f647a1e0)

```
digraph G {
    node [shape=box];

    express -> "accepts";
    express -> "body-parser";
    express -> "content-disposition";
    express -> "content-type";
    express -> "cookie";
    express -> "cookie-signature";
    express -> "debug";
    express -> "depd";
    express -> "encodeurl";
    express -> "etag";
    express -> "finalhandler";
    express -> "fresh";
    express -> "http-errors";
    express -> "merge-descriptors";
    express -> "methods";
    express -> "mime-types";
    express -> "on-finished";
    express -> "once";
    express -> "parseurl";
    express -> "qs";
    express -> "range-parser";
    express -> "router";
    express -> "safe-buffer";
    express -> "send";
    express -> "serve-static";
    express -> "setprototypeof";
    express -> "statuses";
    express -> "type-is";
    express -> "utils-merge";
    express -> "vary";
}
```
![изображение](https://github.com/user-attachments/assets/08768d59-67cb-4088-911a-683edf7d5e2d)

```
digraph G {
    node [shape=box];


    matplotlib -> "contourpy" -> "numpy";
    matplotlib -> "cycler";
    matplotlib -> "fonttools";
    matplotlib -> "kiwisolver";
    matplotlib -> "numpy";
    matplotlib -> "packaging";
    matplotlib -> "pillow";
    matplotlib -> "pyparsing";
    matplotlib -> "python-dateutil" -> six;
}
```
![изображение](https://github.com/user-attachments/assets/72e70821-1416-4e63-931d-0982ce29e7ac)

## Задание 4
```
include "globals.mzn";  % Импорт библиотеки с all_different

% Массив для представления 6-значного билета
array[1..6] of var 0..9: ticket;

% Все цифры должны быть различны
constraint all_different(ticket);

% Сумма первых трёх цифр должна быть равна сумме последних трёх цифр
constraint ticket[1] + ticket[2] + ticket[3] = ticket[4] + ticket[5] + ticket[6];

% Минимизируем сумму трёх цифр (чтобы найти минимальный билет)
var int: sum_3_digits = ticket[1] + ticket[2] + ticket[3];

% Найти минимальную сумму
solve minimize sum_3_digits;
```
![изображение](https://github.com/user-attachments/assets/51907183-2fb4-47b9-97da-027fedcbe456)

## Задание 5
```
% Определение версий с уникальными именами
enum VersionsMenu = { menu_v1_0_0, menu_v1_1_0, menu_v1_2_0, menu_v1_3_0, menu_v1_4_0, menu_v1_5_0 };
enum VersionsDropdown = { dropdown_v1_8_0, dropdown_v2_0_0, dropdown_v2_1_0, dropdown_v2_2_0, dropdown_v2_3_0 };
enum VersionsIcons = { icons_v1_0_0, icons_v2_0_0 };

% Переменные для выбранных версий
var VersionsMenu: menu_version;
var VersionsDropdown: dropdown_version;
var VersionsIcons: icons_version;

% Зависимости версий
constraint
    if menu_version = menu_v1_5_0 then dropdown_version in {dropdown_v2_3_0, dropdown_v2_2_0} /\ icons_version = icons_v2_0_0
    elseif menu_version = menu_v1_4_0 then dropdown_version in {dropdown_v2_2_0, dropdown_v2_1_0} /\ icons_version = icons_v2_0_0
    elseif menu_version = menu_v1_3_0 then dropdown_version in {dropdown_v2_1_0, dropdown_v2_0_0} /\ icons_version = icons_v1_0_0
    elseif menu_version = menu_v1_2_0 then dropdown_version in {dropdown_v2_0_0, dropdown_v1_8_0} /\ icons_version = icons_v1_0_0
    elseif menu_version = menu_v1_1_0 then dropdown_version = dropdown_v1_8_0 /\ icons_version = icons_v1_0_0
    else dropdown_version = dropdown_v1_8_0 /\ icons_version = icons_v1_0_0
    endif;

% Минимизация версии root, которая зависит от версии menu
solve minimize menu_version;
```
![изображение](https://github.com/user-attachments/assets/44ade8f2-5ef3-454e-9d1d-cf384c029bd6)

### Задание 6
```
% Определяем версии для каждого пакета
enum VersionsFoo = { foo_v1_0_0, foo_v1_1_0 };
enum VersionsLeft = { left_v1_0_0 };
enum VersionsRight = { right_v1_0_0 };
enum VersionsShared = { shared_v1_0_0, shared_v2_0_0 };
enum VersionsTarget = { target_v1_0_0, target_v2_0_0 };
enum VersionsRoot = { root_v1_0_0 };

% Переменные для выбранных версий пакетов
var VersionsFoo: foo_version;
var VersionsLeft: left_version;
var VersionsRight: right_version;
var VersionsShared: shared_version;
var VersionsTarget: target_version;
var VersionsRoot: root_version;

% Зависимость root от foo и target
constraint
    root_version = root_v1_0_0 /\
    foo_version in {foo_v1_0_0, foo_v1_1_0} /\
    target_version in {target_v2_0_0};

% Зависимость foo 1.1.0 от left и right
constraint
    if foo_version = foo_v1_1_0 then
        left_version = left_v1_0_0 /\
        right_version = right_v1_0_0
    else
        true
    endif;

% Зависимость left 1.0.0 от shared >= 1.0.0
constraint
    if left_version = left_v1_0_0 then
        shared_version in {shared_v1_0_0, shared_v2_0_0}
    else
        true
    endif;

% Зависимость right 1.0.0 от shared < 2.0.0
constraint
    if right_version = right_v1_0_0 then
        shared_version = shared_v1_0_0
    else
        true
    endif;

% Зависимость shared 1.0.0 от target >= 1.0.0
constraint
    if shared_version = shared_v1_0_0 then
        target_version in {target_v1_0_0, target_v2_0_0}
    else
        true
    endif;

% Решение задачи
solve satisfy;
```
![изображение](https://github.com/user-attachments/assets/58bca0d8-94a9-4355-a53b-f364696c3e3c)

## Задание 7
```
# Структура данных для хранения пакетов и их зависимостей
packages = {
    'root': {
        '1.0.0': {
            'dependencies': {
                'foo': '^1.0.0',
                'target': '^2.0.0'
            }
        }
    },
    'foo': {
        '1.1.0': {
            'dependencies': {
                'left': '^1.0.0',
                'right': '^1.0.0'
            }
        },
        '1.0.0': {
            'dependencies': {}
        }
    },
    'left': {
        '1.0.0': {
            'dependencies': {
                'shared': '>=1.0.0'
            }
        }
    },
    'right': {
        '1.0.0': {
            'dependencies': {
                'shared': '<2.0.0'
            }
        }
    },
    'shared': {
        '2.0.0': {
            'dependencies': {}
        },
        '1.0.0': {
            'dependencies': {
                'target': '^1.0.0'
            }
        }
    },
    'target': {
        '2.0.0': {
            'dependencies': {}
        },
        '1.0.0': {
            'dependencies': {}
        }
    }
}


# Функция проверки совместимости версии пакетов
def check_dependencies(package, version, resolved, packages):
    # Если пакет уже добавлен в решение, пропускаем
    if package in resolved:
        return True

    # Получаем зависимости для указанной версии
    dependencies = packages[package][version]['dependencies']

    for dep_pkg, dep_version in dependencies.items():
        # Проверка совместимости версии зависимостей
        if not resolve_version(dep_pkg, dep_version, packages, resolved):
            return False

    # Добавляем текущий пакет в решенные
    resolved[package] = version
    return True


# Функция выбора совместимой версии
def resolve_version(package, version_range, packages, resolved):
    # Для простоты обрабатываем только некоторые форматы версий
    if version_range.startswith('^'):
        min_version = version_range[1:]  # Минимальная версия для диапазона "^"
        for version in packages[package]:
            if version >= min_version and package not in resolved:
                if check_dependencies(package, version, resolved, packages):
                    return True
    return False


# Основная функция для решения задачи
def solve(packages):
    resolved = {}
    root_version = '1.0.0'  # Задаем корневую версию
    if check_dependencies('root', root_version, resolved, packages):
        print("Решение найдено:", resolved)
    else:
        print("Решение не найдено")


solve(packages)
```
![изображение](https://github.com/user-attachments/assets/5bd279c9-e465-42c2-b9a8-066485ef0fc1)