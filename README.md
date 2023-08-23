## Integración de Tailwind CSS en Proyecto ASP.NET Core MVC

Este tutorial te guiará a través de los pasos para integrar Tailwind CSS en un proyecto ASP.NET Core MVC.

### Paso 1:
Crea el proyecto en Visual Studio o en la interfaz de línea de comandos (dotnet CLI).

### Paso 2:
Inicia un proyecto de Node.js.

```bash
npm init -y
```

### Paso 3:
Agrega Tailwind CSS como dependencia de desarrollo.

```bash
npm install -D tailwindcss
```

### Paso 4:
Agrega un script al archivo `package.json` para definir la ubicación de salida del archivo CSS.

```json
"scripts": {
    "css:build": "npx tailwindcss -i ./wwwroot/css/site.css -o ./wwwroot/css/styles.css --minify"
}
```

### Paso 5:
Inicializa el archivo de configuración de Tailwind.

```bash
npx tailwindcss init
```

### Paso 6:
Agrega módulos al archivo `tailwind.config.js`. Esto es para que Tailwind aplique estilos a las páginas Razor:

```javascript
module.exports = {
    content: [
       './Pages/**/*.cshtml',
       './Views/**/*.cshtml'
    ],
    theme: {
        extend: {},
    },
    plugins: [],
}
```

### Paso 7:
Agrega estilos de entrada al archivo `site.css` en la carpeta `wwwroot/css`.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Paso 8:
Agrega grupos de elementos (`ItemGroups`) en el archivo `.csproj` del proyecto. Esto se hace para construir el CSS antes de implementarlo:

```xml
<ItemGroup>
  <UpToDateCheckBuilt Include="wwwroot/css/site.css" Set="Css" />
  <UpToDateCheckBuilt Include="tailwind.config.js" Set="Css" />
</ItemGroup>

<Target Name="Tailwind" BeforeTargets="Build">
  <Exec Command="npm run css:build"/>
</Target>
```

### Paso 9:
Incluye la ruta al archivo CSS en el archivo `_Layout.cshtml` (o en las vistas que necesites estilizar con Tailwind).

```html
<link rel="stylesheet" href="~/css/styles.css" asp-append-version="true" />
```
