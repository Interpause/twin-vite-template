# twin-vite-template

A Preact framework template that uses the following:

- Vite with HMR
- twin.macro
- Yarn 2 Zero-Installs

Representative of my ideal developer experience.

## Some Gotchas

### Babel Plugins

Yarn 2 especially strict dependency management when using Zero-Installs (and consequentially, Plug'n'Play) means Babel plugins such as `@babel/plugin-transform-react-jsx` must be declared as direct dependencies. This is inspite of these plugins already having been installed as indirect dependencies from, for example, `@preact/preset-vite`.

### Multi-platform Zero Installs

Certain packages resolve differentially depending on the platform, be it `win32` or `linux`. For example, `esbuild` depends on `esbuild-linux-64` on `linux` but instead depends on `esbuild-windows-64` on `win32`. Hence, when switching between platforms, it has to retrieve said dependencies from online (violating Zero Installs), and will delete dependencies meant for other platforms. The official way to solve this is to specify `supportedArchitectures` in `.yarnrc.yml`:

```yaml
# .yarnrc.yml
supportedArchitectures:
  os:
    - linux
    - win32
    - darwin
```
