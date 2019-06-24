### 数据代理

```
class Aue {
    constructor(options) {
        this.$options = options
        this._data = options.data
        Object.keys(this._data).forEach(key => {
            this._proxy(key)
        })
    }
    _proxy(key) {
        Object.defineProperty(this, key, {
            configurable: false,
            enumerable: true,
            get() {
                return this._data[key]
            },
            set(value) {
                this._data[key] = value
            }
        })
    }
}
```