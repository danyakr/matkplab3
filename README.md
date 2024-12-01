# Практическая работа 3 – развитие игры “Инопланетное вторжение”
### Цель работы: Дополнить базовую игру “Инопланетное вторжение” функциональностью, которая сделает игровой процесс более увлекательным и технологичным. В этой работе вы добавите звуковые эффекты, систему уровней, сохранение прогресса и интерактивные объекты с интересными механиками.

### 1. Звуковые эффекты
*Для улучшения восприятия были добавлены звуковые эффекты:*  

Звук выстрела (shot.wav) при активации пули.  
Звук уничтожения пришельцев (explosion.wav).  
Звук потери жизни (life_lost.wav).  
Звук завершения игры (game_over.wav).  

Работа с аудио организована через модуль pygame.mixer.

### 2. Система уровней
Добавлена механика повышения уровня сложности.

*Реализация:*

Переход на новый уровень: происходит при уничтожении всех инопланетян.  
Изменение параметров: с каждым уровнем скорость врагов увеличивается на фиксированный коэффициент.  
Очистка экрана: удаляются оставшиеся пули, создаётся новый флот врагов.  
Ключевые изменения уровня осуществляются через функцию level_up.  

### 3. Сохранение и загрузка прогресса
Для сохранения состояния игры реализована сериализация с помощью модуля pickle. 

*Сохраняемые данные включают:*  
текущий уровень,  
очки,  
количество оставшихся жизней,
скорости.  

*Функции:*  
save_game() — сохраняет данные в файл.  
load_game() — загружает сохранённые данные.  

*Управление осуществляется клавишами:*
S — сохранение игры,  
L — загрузка.  

### 4. Интерактивные объекты с интересными механиками
Добавлены бонусы, предоставляющие игроку дополнительные возможности. 

*Реализован класс Bonus, поддерживающий два типа:*
life — добавляет жизнь,  
shield — активирует временный щит.  

*Основные особенности:*
Появление бонусов: генерируются с заданной вероятностью (bonus_chance) после уничтожения пришельцев.  
Скорость: объекты падают с фиксированной скоростью.  

*Механика взаимодействия при сборе бонуса:*
life увеличивает количество жизней,  
shield защищает корабль от столкновений на ограниченное время.  

### 5. Сборка игры в исполняемый файлен

*Относительные пути для ресурсов*

Для корректной работы в режиме разработки и в собранном приложении реализована функция:
```
def resource_path(relative_path):
    """Определяет абсолютный путь к ресурсу, независимо от того, где запущен файл."""
    try:
        # Для PyInstaller
        base_path = sys._MEIPASS
    except Exception:
        # Для нормальной работы в разработке
        base_path = os.path.abspath(".")
    return os.path.join(base_path, relative_path)
```

*Установка PyInstaller*  
```
pip install pyinstaller
```

*Создание исполняемых файлов*  
Для каждой операционной системы создан отдельный скрипт сборки.  

• Windows  
*build_windows.bat*  
```
@echo off
pyinstaller --onefile --add-data "sounds;sounds" --add-data "images;images" main.py
pause
```

• macOS  
*build_macos.sh*  
```
#!/bin/bash
pyinstaller --onefile --add-data "resources:resources" main.py
```
Сделайте скрипт исполняемым и запустите его:
```
chmod +x build_macos.sh
./build_macos.sh
```

• Linux  
*build_linux.sh*  
```
#!/bin/bash
pyinstaller --onefile --add-data "resources:resources" main.py
```
Сделайте скрипт исполняемым и запустите его:
```
chmod +x build_linux.sh
./build_linux.sh
```

Результатом выполнения скриптов станет исполняемый файл игры, расположенный в папке dist.



