## Class: BrowserView

> Создание и Управление видами.

**Примечание:** BrowserView API в настоящее время экспериментально и может измениться или быть удалено в будущих релизах Electron.

Process: [Main](../glossary.md#main-process)

`BrowserView` может использоваться для внедрения дополнительного веб-содержимого в `BrowserWindow`. Это как дочернее окно, за исключением того, что оно позиционируется относительно его владельца окна. Он предназначен для того, чтобы быть альтернативой тега `webview`.

## Пример

```javascript
// В основном процессе.
const {BrowserView, BrowserWindow} = require('electron')

let win = new BrowserWindow({width: 800, height: 600})
win.on('closed', () => {
  win = null
})

let view = new BrowserView({
  webPreferences: {
    nodeIntegration: false
  }
})
win.setBrowserView(view)
view.setBounds({ x: 0, y: 0, width: 300, height: 300 })
view.webContents.loadURL('https://electronjs.org')
```

### `new BrowserView([options])` *Экспериментально*

* `options` Object (опционально) 
  * `webPreferences` Объект (опционально) - см. [BrowserWindow](browser-window.md).

### Статические методы

#### `BrowserView.getAllViews()`

Returns `BrowserView[]` - An array of all opened BrowserViews.

#### `BrowserView.fromWebContents(webContents)`

* `webContents` [WebContents](web-contents.md)

Returns `BrowserView | null` - The BrowserView that owns the given `webContents` or `null` if the contents are not owned by a BrowserView.

#### `BrowserView.fromId(id)`

* `id` Integer

Возвращает `BrowserView` - вид с заданным `id`.

### Instance Properties

Объекты, созданные с помощью `new BrowserView`, имеют следующие свойства:

#### `view.webContents` *Экспериментально*

Объект [`WebContents`](web-contents.md), принадлежащий этому виду.

#### `view.id` *Экспериментально*

`Integer`, представляющий уникальный идентификатор вида.

### Методы экземпляра

Объекты, созданные с помощью `new BrowserView`, имеют следующие свойства:

#### `view.setAutoResize(options)` *Экспериментально*

* `options` Object 
  * `width` Boolean - если `true`, то ширина будет увеличиваться и уменьшаться вместе с окном. По умолчанию `false`.
  * `height` Boolean - если `true`, то высота будет увеличиваться и уменьшаться вместе с окном. По умолчанию `false`.

#### `view.setBounds(bounds)` *Экспериментально*

* `bounds` [Rectangle](structures/rectangle.md)

Изменяет и перемещает вид в предоставленные границы относительно окна.

#### `view.setBackgroundColor(color)` *Экспериментально*

* `color` String - цвет вида `#aarrggbb` или `#argb`. Альфа-канал является опциональным.