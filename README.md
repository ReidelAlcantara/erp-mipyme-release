# ERP MIPYME — Canal de Releases

> **Canal público de distribución** del ERP MIPYME: sistema de gestión
> offline-first para MIPYMES cubanas de ventas mayoristas y minoristas.
> El código fuente completo vive en un repositorio **privado**; aquí se
> publica lo que el cliente final necesita descargar.

## Qué es el ERP MIPYME

Sistema ERP multiplataforma (**Windows + Android**) diseñado para operar
**100% sin conexión** — requisito esencial en entornos con conectividad
intermitente — y sincronizarse de forma transparente cuando hay red:

| Módulo | Capacidades |
|---|---|
| **POS (punto de venta)** | Venta offline, impresión ESC/POS de comprobantes, numeración por dispositivo |
| **Contabilidad cubana** | Resolución 494/2016: partida doble, diario, mayor, cierre de ejercicio, CUP |
| **Inventario** | Mínimos con alertas, kardex de entradas/salidas, costo promedio ponderado |
| **RRHH** | Fichas de empleados y control de asistencia |
| **Seguridad** | Usuarios + PIN, roles: Admin / Dependiente / Económico / Almacenero |
| **Sincronización** | SQLite local (op-sqlite) ↔ PowerSync ↔ PostgreSQL en Neon |

Tecnología: React Native 0.75 + TypeScript estricto, Clean Architecture +
MVVM, PowerSync, estilo visual "futuro neón".

## 📥 Descargas

Ir a la pestaña [**Releases**](../../releases). Cada release incluye:

- `erp-mipyme-vX.Y.Z-src.zip` — código fuente completo verificable
  (aplicación + backend + documentación + pruebas).
- `erp-mipyme-vX.Y.Z-android.apk` — **APK Android firmado listo para
  instalar** (instalación directa: habilitar "orígenes desconocidos").
- Archivos `SHA256SUMS` para verificar la integridad de cada descarga.

### Verificar integridad (recomendado)

```bash
sha256sum erp-mipyme-v1.0.0-*.zip erp-mipyme-v1.0.0-*.apk
# comparar contra los valores publicados en el archivo SHA256SUMS correspondiente
```

En Windows PowerShell:

```powershell
Get-FileHash .\erp-mipyme-v1.0.0-android.apk -Algorithm SHA256
```

## 🏗️ Cómo se compila este canal

Este repositorio contiene dos flujos de trabajo de GitHub Actions
(pestaña **Actions**), ambos de disparo manual:

1. **Compilar y Publicar Release** — descarga el código del repositorio
   privado, ejecuta las verificaciones de calidad (`npm ci`,
   `tsc --noEmit` en modo estricto, suite Jest de Dominio + Casos de Uso),
   empaqueta el código fuente y publica la release con sus sumas SHA-256.
2. **Compilar APK Android** — monta el proyecto Android sobre la base
   oficial de React Native 0.75.4, compila con Gradle (`assembleRelease`)
   y firma el APK con la clave de distribución del proyecto.

## 📱 Instalación del APK

1. Descarga `erp-mipyme-vX.Y.Z-android.apk` desde la release.
2. En el dispositivo Android: habilita *Instalar apps desconocidas* para
   tu navegador o gestor de archivos.
3. Abre el APK e instala.
4. En el primer arranque, el sistema guía la configuración inicial
   (usuario Administrador con PIN y siembra del nomenclador contable).

> **Nota sobre la firma:** el APK se firma con la clave de distribución
> del proyecto. Las actualizaciones futuras publicadas por este canal
> instalarán directamente sobre la versión anterior. Para publicar en
> Google Play se recomienda generar una clave propia (ver
> `docs/04-INSTALACION.md` dentro del ZIP).

## 🔒 Privacidad del código fuente

Este repositorio **no contiene código fuente de la aplicación**: solo la
automatización de compilación y publicación. Así se protege la propiedad
intelectual del desarrollo mientras el canal de descarga permanece
público para clientes y distribuidores.

## 📞 Soporte

Canal de soporte y licenciamiento: propietario del proyecto
(**Reidel Alcantara**). Para reportes de fallas del APK, indicar versión
(ver pie de pantalla "Acerca de" dentro de la app) y adjuntar el registro
de errores exportable desde la propia aplicación.
