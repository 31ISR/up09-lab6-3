# Лабораторная работа 6-3

## Дедлайн сдачи работы без пенальти

???

## Как выполнять

- Создать ветку `mod-3` из ветки `mod-2`

- Открыть ветку `mod-3` в workspace

## Генерация контроллера

1. Создайте контроллер для заметками

```bash
php artisan make:controller NoteController --resource --model=Note
```

Создает контроллер для работы с заметками `app/Http/Controllers/NoteController.php`

2. Измените методы работы с моделью (`index`, `create`, `show`, `edit`)

```bash
{
    return 'index'
}
```

_Вместо `index` должно быть название метода_

3. Создайте маршрутизацию для этих методов в файле `routes/web.php`

```php
Route::get('/note', [NoteController::class, 'index'])->name('note.index');
Route::get('/note/create', [NoteController::class, 'create'])->name('note.create');
Route::post('/note', [NoteController::class, 'store'])->name('note.store');
Route::get('/note/{id}', [NoteController::class, 'show'])->name('note.show');
Route::get('/note/{id}/edit', [NoteController::class, 'edit'])->name('note.edit');
Route::put('/note/{id}', [NoteController::class, 'update'])->name('note.update');
Route::delete('/note/{id}', [NoteController::class, 'destroy'])->name('note.destroy');
```

_Протестируйте эти маршруты (например, `localhost:8000/note/create` и тд (должны показываться названия роутов, которые вы писали в `return`))_

> [!warning]
> Создайте роуты под работу с тудушками
> Необходимые роуты
> |Метод|маршрут|Название|
> |-|-|-|
> |get|`/todo`|index|
> |get|`/todo/create`|create|
> |post|`/todo`|store|
> |get|`/todo/{id}`|show|
> |get|`/todo/{id}/edit`|edit|
> |put|`/todo/{id}`|update|
> |delete|`/todo/{id}`|destroy|

### Апдейты контроллера

1. Измените маршрутизацию на сокращенный синтаксис (закомментируйте старый код)

```php
Route::resource('note', NoteController::class);
```

_Обязательно проверьте, что роуты работают_

> [!warning]
> Измените роуты todo на сокращенный синтаксис под работу с тудушками

2. Добавить представления для заметок

Создаем 3 представления (index, edit, show) в папке `resources/view/note` при помощи artisan

```bash
php artisan make:view note.index
php artisan make:view note.edit
php artisan make:view note.show
php artisan make:view note.create
```

3. В каждое представление добавьте `h1` заголовок с названием представления

4. Найдите в контроллере заметок роуты, которые отвечают за эти 4 маршрута и измените, чтобы они возвращали представления

_например для index - меняйте только строчку с return_

```php
public function index()
{
    return view('note.index');
}
```

> [!warning]
> Создайте маршруты и представления под работу с тудушками. Также добавьте h1 заголовки с названием маршрута в каждый из них
>
> Необходимые представления:
>
> - index
> - edit
> - show
> - create

### Создание шаблона для страниц представления

1. Создайте файл `resources/views/components/layout.blade.php`

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />

        <title>Laravel</title>

        @vite(['resources/css/app.css', 'resources/js/app.js'])
    </head>

    <body class="antialiased">
        {{ $slot }}
    </body>
</html>
```

- Где slot - контент, которые будет помещен между тегами `x-layout`,
- где `x` - компонент,
- а `layout` название компонента

2. Используйте шаблон в index.blade.php

```php
<x-layout>
    <h1>index</h1>
</x-layout>
```

> [!warning]
> Утилизируйте шаблон во всех представлениях
