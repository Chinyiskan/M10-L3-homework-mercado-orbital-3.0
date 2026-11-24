<div align="center">

# 🛰️ Mercado Orbital 3.0

### 📋 Ticket MO-302 · Home Challenge: Zona del hangar

![Puntos](https://img.shields.io/badge/valor-15%20puntos-2EA44F?style=for-the-badge)
![Tiempo](https://img.shields.io/badge/tiempo-40%20min-FF9800?style=for-the-badge)
![Entrega](https://img.shields.io/badge/entrega-link%20de%20GitHub%20en%20Notion-0A66C2?style=for-the-badge&logo=github&logoColor=white)

<img src="assets/nova-lectura.webp" width="360" alt="Nova lee en un sillón con audífonos mientras Kuma duerme a su lado">

</div>

---

## 🚀 Misión

> 👩‍🚀 **Nova:** Kuma quiere su rincón en el Mercado Orbital: una zona con la lista de reparaciones. Ahí no va el encabezado de la tienda ni el carrito. Quiero un menú lateral y un botón para volver al mostrador.

<div align="center">

<img src="assets/kuma-hangar.webp" width="220" alt="Kuma, el robot araña de Nova, moviendo las patas">

</div>

La zona del hangar tiene su propio layout: un menú lateral en vez del encabezado de la tienda. Las páginas se pintan en su `Outlet`, igual que en `LayoutTienda`. El kit de la clase ya trajo los estilos (en `App.css`), los datos de las reparaciones (`src/data/reparaciones.js`) y las imágenes (`public/img/hangar/`).

Sigues en tu **Mercado Orbital 3.0** de la clase, con los cuatro tickets de MO-301 resueltos. No se crea un proyecto nuevo.

| 🧭 Ruta | 📄 Página | 🧱 Layout |
| --- | --- | --- |
| `/hangar` | `PaginaHangar` | `LayoutHangar` |
| `/hangar/reparaciones` | `PaginaReparaciones` | `LayoutHangar` |

## 🏆 Tablero de puntos

| Ticket | Qué haces | Puntos |
| --- | --- | :---: |
| 1️⃣ | LayoutHangar | 🟢 5 |
| 2️⃣ | Rutas del hangar | 🟡 6 |
| 3️⃣ | Ida y vuelta | 🟠 4 |
| 🌟 | Extra para curiosos | ⭐ 0 |
| | **Total** | **15** |

---

## 🎫 Tickets

### 1️⃣ Ticket 1 · LayoutHangar (5 puntos)

📄 Archivos: `src/components/LayoutHangar.jsx` (nuevo) y `src/App.jsx`.

1. Crea `LayoutHangar`, un componente sin props que devuelve un `<div className="hangar">`. Importa `Link` y `Outlet` desde `"react-router"`.
2. Dentro, un `<aside className="menu-hangar">` con tres cosas, en este orden:
   - Un `Link` a `"/"` con el texto "Volver a la tienda" y `className="volver-tienda"`.
   - Un título `<h2>Zona del hangar</h2>`.
   - Un `<nav>` con dos `Link`: "Estado del hangar" a `"/hangar"` y "Reparaciones" a `"/hangar/reparaciones"`.
3. Después del `<aside>`, un `<main className="contenido-hangar">` con `<Outlet />` adentro.
4. En `App.jsx`, importa `LayoutHangar` y, dentro de `<Routes>` y después del layout de la tienda, agrega una ruta hermana: `<Route path="hangar" element={<LayoutHangar />} />`. Por ahora sin hijas.
5. Abre `localhost:5173/hangar`.

**🏁 Listo cuando:**

- [ ] `/hangar` muestra el menú lateral con "Volver a la tienda", "Estado del hangar" y "Reparaciones".
- [ ] No aparece el encabezado de la tienda ni el botón del carrito.
- [ ] "Volver a la tienda" lleva a `/` sin recargar la página.

> [!NOTE]
> El contenido sale vacío y "Reparaciones" lleva a la 404 de la tienda. Faltan las rutas hijas, que llegan en el Ticket 2.

### 2️⃣ Ticket 2 · Rutas del hangar (6 puntos)

📄 Archivos: `src/pages/PaginaHangar.jsx` (nuevo), `src/pages/PaginaReparaciones.jsx` (nuevo) y `src/App.jsx`.

1. `PaginaHangar` ya viene escrita: crea `src/pages/PaginaHangar.jsx` y pega esto.

```jsx
function PaginaHangar() {
    return (
        <section>
            <img src="/img/hangar/banner-hangar.webp" alt="Hangar 3 con tres naves en reparación" className="banner-hangar" />
            <h2>Estado del hangar</h2>
            <p>Kuma tiene tres naves en el taller y cuatro reparaciones anotadas. Mira la lista en Reparaciones.</p>
        </section>
    );
}

export default PaginaHangar;
```

2. `PaginaReparaciones` la escribes tú: importa `reparaciones` desde `"../data/reparaciones.js"`, pinta un `<h2>Reparaciones</h2>` y un `<ul className="lista-reparaciones">`. Con `map` y `key={reparacion.id}`, cada reparación es un `<li className="reparacion">` con este contenido:

```jsx
<img src={reparacion.imagen} alt={reparacion.nave} className="reparacion-nave" />
<div>
    <strong>{reparacion.nave}</strong>
    <span>{reparacion.pieza}</span>
</div>
<span className="reparacion-estado">{reparacion.estado}</span>
```

3. En `App.jsx`, importa `PaginaHangar` y `PaginaReparaciones`. La `Route` de `hangar` pasa a tener hijas: `<Route index element={<PaginaHangar />} />` y `<Route path="reparaciones" element={<PaginaReparaciones />} />`. Las hijas llevan rutas relativas, sin `/` al inicio.

**🏁 Listo cuando:**

- [ ] `/hangar` muestra "Estado del hangar" dentro del layout.
- [ ] `/hangar/reparaciones` muestra las 4 reparaciones, cada una con la imagen de su nave, su nombre, su pieza y su estado.
- [ ] Los enlaces del menú lateral cambian de página sin recargar.
- [ ] La consola no avisa de `key`.

> [!WARNING]
> Si escribes `path="/reparaciones"` dentro de `hangar`, React Router lanza un error de ruta absoluta anidada y la pantalla se queda en blanco. Las hijas van sin `/`.

### 3️⃣ Ticket 3 · Ida y vuelta (4 puntos)

📄 Archivos: `src/components/Encabezado.jsx` y `src/components/LayoutHangar.jsx`.

1. En `Encabezado`, agrega un cuarto `NavLink` (`NavLink` ya está importado ahí desde la clase) al menú de la tienda: "Hangar", con `to="/hangar"`.
2. En `LayoutHangar`, agrega `NavLink` al `import` de `"react-router"` y cambia los dos `Link` del `<nav>` por `NavLink`. El de `"/hangar"` lleva la prop `end`. "Volver a la tienda" se queda como `Link`.

**🏁 Listo cuando:**

- [ ] Desde la tienda, el menú tiene Inicio, Catálogo, Taller y Hangar, y "Hangar" lleva a `/hangar`.
- [ ] En `/hangar` solo "Estado del hangar" está resaltado. En `/hangar/reparaciones`, solo "Reparaciones".
- [ ] Agrega dos repuestos al carrito, entra al hangar, recorre sus dos páginas y vuelve con "Volver a la tienda": el contador sigue en 2.

> [!TIP]
> Quita `end` un momento: en `/hangar/reparaciones` quedan resaltados dos enlaces, porque esa dirección también empieza por `/hangar`. Vuelve a ponerlo.

### 🌟 Extra para curiosos (sin puntos)

Hoy, `/hangar/lo-que-sea` cae en la 404 de la tienda, con el encabezado de la tienda. Haz que la zona del hangar tenga su propia 404: crea un componente `PaginaHangarNoEncontrada` en `src/pages/` y agrégalo como `<Route path="*" element={<PaginaHangarNoEncontrada />} />` dentro de la `Route` de `hangar`. Debe mostrar un aviso corto y un `Link` de vuelta a `/hangar`. Si quieres, usa la imagen `/img/hangar/kuma-perdido.webp` con `className="kuma-perdido"`.

**🏁 Listo cuando:**

- [ ] `/hangar/lo-que-sea` muestra el aviso dentro de `LayoutHangar`, con el menú lateral y sin el encabezado de la tienda.
- [ ] `/repuestos-gratis` sigue mostrando la 404 de la tienda.

---

## 💡 Pistas

- 🧱 `LayoutHangar` se arma igual que `LayoutTienda`: lo fijo alrededor y `<Outlet />` en el hueco.
- 🧭 La ruta de `hangar` tiene `path` porque agrega `/hangar` a la dirección de sus hijas. La de `LayoutTienda` no lo tiene.
- 📋 La lista de reparaciones se arma igual que las tarjetas del catálogo: `map` y `key` con el `id`.
- ✅ `end` hace que un `NavLink` solo se marque en su dirección exacta.

## 📤 Cómo entregar

1. Sube los cambios a tu repositorio de GitHub del Mercado Orbital (`git add .`, `git commit -m "MO-302 zona del hangar"`, `git push`).
2. Pega el link del repositorio en la entrega de Notion de esta semana.
3. Deja `URL_CATALOGO` en `/api/productos.json` antes de subir.

## 📊 Criterios

| Ticket | Qué se revisa | Puntos |
| --- | --- | --- |
| Ticket 1 · LayoutHangar | Existe `src/components/LayoutHangar.jsx` con un menú lateral, un `Link` "Volver a la tienda" a `/` y un `<Outlet />`. La ruta `hangar` en `App.jsx` pinta `LayoutHangar`. En `/hangar` no aparece el encabezado de la tienda. | 5 |
| Ticket 2 · Rutas del hangar | Existen `src/pages/PaginaHangar.jsx` y `src/pages/PaginaReparaciones.jsx`. Son hijas de la `Route` de `hangar`: una con `index` y otra con `path="reparaciones"` (sin `/` al inicio). `PaginaReparaciones` pinta `reparaciones` con `map` y `key`. | 6 |
| Ticket 3 · Ida y vuelta | `Encabezado` tiene un `NavLink` "Hangar" a `/hangar`. El menú lateral usa `NavLink` y el de `/hangar` lleva `end`, de modo que en cada página solo hay un enlace resaltado. | 4 |
| **Total** | | **15** |
| Extra (sin puntos) | Una 404 propia del hangar con `path="*"` dentro de la `Route` de `hangar`: `/hangar/lo-que-sea` se ve dentro de `LayoutHangar`. Se anota como bonus, no suma puntos. | 0 |

> [!IMPORTANT]
> Se descuentan hasta 2 puntos si el proyecto no arranca con `pnpm dev` o si quedaron errores en la consola al recorrer `/hangar` y `/hangar/reparaciones`.
