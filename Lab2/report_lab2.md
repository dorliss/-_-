# Языка программирования для задач искусственного интеллекта
Доренская Елизавета Артёмовна, НПИмд-01-24

## Лабораторная работа №2

#### Задание:
- Установить ROS2 Humble
- Изучить планировщик Pyperplan [Pyperplan Github](https://github.com/aibasel/pyperplan)
- Построить модель среды с tb3 (4) с манипулятором, либо любой другой колесный робот с манипулятором [E-manual for tb3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- Создать ROS узел с планировщиком.

### Подготовительная работа:
- Для выполнения лабораторной работы мной было приняно решение работать Ubuntu (версия 22.04 с графическим интерфейстом). Для этого нужно было скачать iso-образ с официального сайта Ubuntu, а также скачать Oracle VM VirlualBox, чтобы запустить виртуальную машину.
  
- Выбор среды был связан с тем, что ROS2 (Robot Operating System 2) официально поддерживается на Ubuntu, что обеспечивает совместимость и стабильность. Многие инструменты и библиотеки для робототехники, включая Pyperplan, часто разрабатываются с учетом работы на Ubuntu. Также для установки ROS2 можно легко ввести команды в терминале, что очень упрощает процесс.

Результат выполнения:<br /> 
![](pics/1.png)

### Установка ROS2 Humble:
- Проверка локали и установка необходимых пакетов:
```bash
locale  # check for UTF-8
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # verify settings
```

Проверка текущие настройки локали системы до изменений:<br />
![](pics/2.jpg)

Проверка текущие настройки локали системы после изменений (по факту ничего не поменялось, все было так, как нужно):<br />
![](pics/3.jpg)


<!--- 

### 2. Изучить планировщик Pyperplan [Pyperplan Github](https://github.com/aibasel/pyperplan):
- Просматривая документацию по pyperplan, я клонировал его в свою виртуальную среду и установил зависимости. Либо просто выполните ```pip install pyperplan```. <br>
<br>
<img src="images/pyperplanclone.png" alt="Pyperplan Cloned" style="width:800px;"/>
<br>
- Затем я посмотрел на флаги и структуру pyperplan, чтобы проверить, смогу ли я запустить тест внутри него. <br>
<br>
<img src="images/pyperplaninside.png" alt="Pyperplan Flags" style="width:800px;"/>
<br>
- Наконец, я провел тест, чтобы убедиться, что pyperplan работает, запустив домен и задачу. <br>
<br>
<img src="images/pyperplantest.png" alt="Pyperplan Test" style="width:800px;"/>
<br>

### 3- Построить модель среды с tb3 (4) с манипулятором, либо любой другой колесный робот с манипулятором [E-manual for tb3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- Я установил TurtleBot3 с его зависимостями и симуляциями из исходного кода, чтобы убедиться, что не будет никаких проблем. После завершения всех шагов в документации я запустил TurtleBot3 с моделью MODEL=waffle внутри Gazebo в пустом мире, чтобы убедиться, что после этого шага смогу просто запустить его с манипуляторной рукой. <br>
<br>
<img src="images/wafflespawnemptyworld.png" alt="waffle in empty world" style="width:800px;"/>
<br>
- Затем я установил зависимости для манипуляторной руки на TB3 Waffle и запустил её в среде машинного обучения.
<br>
<img src="images/turtlebotwmanipulator.png" alt="waffle in ml env with manipulator hand" style="width:800px;"/>
<br>

### 4- Создать ROS узел с планировщиком.
- Прочитав несколько документаций в интернете, я создал базовый узел ROS2, который просто использует pyperplan без инструкций, чтобы показать, что pyperplan запускается, затем узел вращается и корректно завершает работу. <br>
<br>
<img src="images/pyperplannodeforros2.png" alt="Ros2 Node with Pyperplan" style="width:800px;"/>
<br>

```python
#!/usr/bin/env python3

import rclpy
from rclpy.node import Node
import pyperplan
from rclpy.executors import SingleThreadedExecutor

class SimpleNode(Node):
    def __init__(self):
        super().__init__('pyperplan_node')
        self.get_logger().info('pyperplan is ready on machine doruk@dorukvn...')

        '''
        Here goes the domain and the test etc...
        '''

        self.create_timer(2.0, self.cleanShutdown)
    
    def cleanShutdown(self):
        self.get_logger().info('shutting down')
        rclpy.shutdown()

def main(args=None):
    rclpy.init(args=args)
    node = SimpleNode()
    executor = SingleThreadedExecutor()
    executor.add_node(node)
    try:
        executor.spin()
    except KeyboardInterrupt:
        node.get_logger().info('shutting down: Ki')
    finally:
        node.get_logger().info('cleaning up...')
        executor.shutdown()
        node.destroy_node()

if __name__ == '__main__':
    main()
```
 --->
