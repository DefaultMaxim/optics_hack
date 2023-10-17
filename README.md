# optics_hack
---
# MAD TEAM
---
# Мы команда MAD team рады представить вам наше решение данной задачи.
---
Наше решение включает в себя как оптимизацию определенной, заранее известной схемы, так и генерацию случайной схемы, с последующей ее оптимизацией. 
Это позволяет не зависить от представленных схем, а получать хорошие значения лосса, генерируя оптическую схему самим.

В качестве решения нами был выбран генетический алгоритм - алгоритм, который находит минимум имитируя процесс биологической эволюции. 
Данный алгоритм хорошо подходит для поиска глобального оптимумума. Также, данный алгоритм прекрасно работает со случайными схемами: 
т.е, если у нас стоит задача сгенерировать оптическую схему, мы создаем случайную, а далее уже оптимизируем ее под наши требования. 
Так у нас выходили схемы со значением loss = 8, 11, 12, 13 и тд.
# Структура проекта:
---
1. Файлы random_gen_focus.py и random_gen.py
   * random_gen_focus.py генерирует случайную оптическую схему, не попадая в фокусное расстояние = 5мм., однако с многим лучшим поведением лучей света.
     Генерирует файл random_gen_focus.roa
   
   * random_gen.py генерирует случайную оптическую схему, попадающую в фокусное расстояние = 5мм., однако свет там ведет себя не совсем хорошо.
     Генерирует файл random_gen.roa

2. Файлы оптимизации:
    * multiproc_genetic.py - основной файл оптимизации. Он представляет из себя генетический алгоритм, который оптимизирует файл который вы в него передатите.
     Если лосс < 15, то файлы .roa сохраняются в папку low_loss/loss_значение лосса. Всегда генерирует файл genetic_opt.roa.
    * multiproc_genetic1.py - файл, который не совсем корректно работает, но тоже выдает очень хорошие значения loss, н-р для test.roa было получено значение loss = 8.
      Всегда генерирует файл genetic_opt.roa.
     * ray_optics_criteria_ITMO_optimize_curvature.py Файл, который оптимизирует оптическую схему с помощью scipy minimize
3. Файлы .roa
   * loss8.roa Был получен путем применения scipy minimize к test.roa
   * loss16.roa Был получен путем применения генетического алгоритма к случайной оптической схеме.
   * test.roa Файл из задания.
   * random_gen.roa Файл который плохо ведет себя со светом, но попадает в фокус.
   * random_gen_focus.roa Схема которая хорошо попадает в фокус.
   * genetic_opt.roa Генерируется и перезаписывается по мере работы генетического алгоритма (сохраняет последний лосс).
4. Утилиты
   * ray_optics_criteria_ITMO.py Модифицированный файл который был дан. Удалены все принты, и все плоты.
     Считает лосс. Если лосс меньше опеределенного значения (по умолчанию = 600), то сохраняет в папку low_loss/loss_{loss}.
---
# Описание работы:
---
Первый запуск:

Установите все библиотеки из requirements.txt (pip install -r requirements.txt), 
далее откройте файл multiproc_genetic.py измените путь до файла (по дефолту оптимизируется random_gen_focus.roa), который хотите оптимизировать, измените параметры модели (по желанию). 
Для использования многопоточности запускайте файл через консоль (требуется scoop): 
1. cmd
2. cd path
3. py -m scoop multiproc_genetic.py

В конце работы алгоритма создадутся папки low_loss и best, по сути это одно и то же.

Лучше заходите в папку low_loss, там собираются модели с loss < значения (по умолчанию = 600) см. Структура проекта 4.1.
Оптические схемы в папке low_loss называются loss_{значение лосса}.

Для запуска с другими параметрами, или оптимизацией другого файла - переходите в multiproc_genetic.py и меняйте нужные вам параметры.

Мы постарались сделать рассказ о нашей моеделе и о ее способах запуска максимально понятным и простым, спасибо за задачу, было очень инетересно ее решать!

Если у вас появятся вопросы будем рады ответить E-mail: maksim.egorov1@yandex.ru, tg: @[klop1007](https://t.me/klop1007)
