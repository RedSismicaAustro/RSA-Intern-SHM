# RSA Intern SHM

Repositorio para la **migración de proyectos electrónicos desde Altium Designer hacia KiCad 10** desarrollados para el sistema **RSA Structural Health Monitoring (SHM)**.

El propósito de este repositorio es preservar los diseños electrónicos existentes, reemplazar las bibliotecas propietarias utilizadas en Altium por bibliotecas locales compatibles con KiCad y establecer un flujo de trabajo estandarizado para el mantenimiento del hardware mediante herramientas de código abierto.

Como parte del proceso de migración, cada proyecto es revisado para verificar la integridad del esquemático y del PCB, actualizar las bibliotecas de símbolos y huellas, asociar modelos tridimensionales, asignar códigos **LCSC** a los componentes compatibles con **JLCPCB** y generar nuevamente todos los archivos necesarios para fabricación y ensamblaje automático.

La documentación específica de cada tarjeta se encuentra en la carpeta **Docs**, mientras que las bibliotecas compartidas se almacenan dentro de **KiCad/libs**, permitiendo reutilizar componentes entre diferentes proyectos y garantizando que cualquier desarrollador pueda abrir los diseños sin depender de configuraciones locales.

---

# Objetivos

El proceso de migración busca establecer una metodología uniforme para todos los proyectos electrónicos del sistema SHM. Los principales objetivos del repositorio son:

- Migrar los diseños electrónicos desde Altium Designer hacia KiCad 10.
- Eliminar dependencias de bibliotecas propietarias.
- Centralizar símbolos, footprints y modelos 3D en bibliotecas locales.
- Mantener todos los proyectos bajo control de versiones mediante Git.
- Preparar los diseños para fabricación y ensamblaje mediante JLCPCB.
- Documentar el proceso de migración para facilitar futuras modificaciones y revisiones.

---

# Estructura del repositorio

El repositorio se organiza de manera que cada proyecto conserve su propia documentación, mientras que las bibliotecas compartidas permanecen centralizadas para facilitar su reutilización.

```text
RSA-Intern-SHM/
│
├── Docs/
│   ├── Nodo/
│   │   └── README.md
│   ├── Concentrador/
│   │   └── README.md
│   ├── Concentrador2/
│   │   └── README.md
│   └── ...
│
├── KiCad/
│   ├── libs/
│   │   ├── RSA.kicad_sym
│   │   ├── RSA.pretty/
│   │   ├── LibExt.pretty/
│   │   └── packages3d/
│   │
│   └── projects/
│       ├── Nodo/
│       ├── Concentrador/
│       ├── Concentrador2/
│       └── ...
│
├── Firmware/
│
├── Production/
│
└── README.md
```

La carpeta `KiCad/projects` contiene los proyectos electrónicos migrados, mientras que `KiCad/libs` almacena todas las bibliotecas compartidas utilizadas por los diferentes diseños. Esta organización evita duplicar componentes y simplifica el mantenimiento de las bibliotecas a medida que nuevos proyectos son incorporados al repositorio.

---

# Herramientas utilizadas

La migración y mantenimiento de los proyectos se realiza utilizando herramientas de código abierto y utilidades complementarias para automatizar la generación de bibliotecas y archivos de fabricación.

| Herramienta | Descripción |
|-------------|-------------|
| KiCad 10 | Diseño y edición de esquemáticos y PCB |
| Python 3 | Automatización de herramientas auxiliares |
| Git | Control de versiones |
| JLC2KiCadLib | Descarga automática de símbolos, footprints y modelos 3D |
| Fabrication Toolkit | Generación de BOM, CPL, Gerbers y NC Drill |
| JLCPCB | Fabricación y ensamblaje PCBA |

---

# Flujo de migración

Todos los proyectos contenidos en este repositorio siguen un procedimiento de migración común con el objetivo de mantener una estructura uniforme y facilitar el mantenimiento futuro.

El proceso comienza con la importación del proyecto desde Altium Designer hacia KiCad. Posteriormente se realiza una revisión completa del esquemático y del PCB para verificar que las conexiones eléctricas, las referencias de componentes y las reglas de diseño hayan sido importadas correctamente.

Una vez validado el diseño, se sustituyen las bibliotecas originales por bibliotecas locales compatibles con KiCad. Cada símbolo queda asociado con su respectiva huella y, cuando está disponible, con su modelo tridimensional.

Posteriormente se revisan los componentes para identificar aquellos compatibles con el servicio PCBA de JLCPCB. A estos componentes se les asigna su correspondiente código LCSC, permitiendo automatizar la generación de la lista de materiales y del archivo de posicionamiento durante el proceso de fabricación.

Finalmente se ejecutan las verificaciones ERC y DRC, se generan los archivos Gerber, NC Drill, BOM y CPL mediante Fabrication Toolkit y se valida la documentación obtenida utilizando el visor de JLCPCB.

---

# Organización de bibliotecas

Uno de los principales objetivos de la migración consiste en eliminar la dependencia de bibliotecas instaladas globalmente. Para ello, todos los símbolos, footprints y modelos tridimensionales utilizados por los proyectos se almacenan dentro del repositorio.

Las bibliotecas principales utilizadas son:

- RSA.kicad_sym
- RSA.pretty
- LibExt.pretty

Los modelos tridimensionales asociados a cada componente se almacenan dentro de la carpeta `packages3d`, mientras que los componentes descargados automáticamente desde JLCPCB se incorporan a las bibliotecas locales mediante **JLC2KiCadLib**.

Esta organización garantiza que cualquier proyecto pueda abrirse correctamente después de clonar el repositorio, independientemente del equipo utilizado.

---

# Proyectos

Actualmente el repositorio contiene varias tarjetas electrónicas migradas desde Altium Designer hacia KiCad 10.

| Proyecto | Descripción |
|-----------|-------------|
| Nodo | Nodo de adquisición de datos del sistema SHM. |
| Concentrador | Tarjeta concentradora de comunicaciones. |
| Concentrador2 | Segunda revisión del concentrador con mejoras de hardware. |

Cada proyecto dispone de un archivo `README.md` independiente dentro de la carpeta `Docs`, donde se documenta el procedimiento de migración, la configuración de bibliotecas, la lista de componentes, los códigos LCSC y el proceso de generación de archivos de fabricación.

---

# Preparación para fabricación

Todos los diseños fueron preparados para ser fabricados utilizando el servicio **JLCPCB PCBA**. Los componentes compatibles emplean códigos **LCSC**, permitiendo automatizar la generación de la lista de materiales y el posicionamiento de componentes durante el ensamblaje.

Antes de generar los archivos de producción se revisan las propiedades de cada componente para configurar correctamente las opciones **Exclude from BOM** y **Exclude from Board**, evitando que conectores, elementos mecánicos o componentes de montaje manual sean incluidos en los archivos de ensamblaje.

La documentación de fabricación generada para cada proyecto incluye:

- Gerber
- NC Drill
- Bill of Materials (BOM)
- Component Placement List (CPL)

Estos archivos pueden almacenarse dentro de la carpeta `Production` correspondiente a cada diseño para facilitar futuras órdenes de fabricación.

---

# Buenas prácticas

Para mantener la consistencia del repositorio se recomienda utilizar exclusivamente las bibliotecas locales almacenadas en `KiCad/libs` y evitar referencias a bibliotecas instaladas globalmente. Asimismo, cualquier componente nuevo debe incorporar su correspondiente símbolo, huella y modelo tridimensional antes de ser utilizado en un proyecto.

Se recomienda ejecutar las verificaciones ERC y DRC antes de cada liberación, mantener actualizados los códigos LCSC de los componentes compatibles con JLCPCB y validar los archivos Gerber, BOM y CPL utilizando el visor web del fabricante antes de confirmar una orden de producción.

Toda modificación realizada sobre un proyecto o una biblioteca debe registrarse mediante Git para conservar el historial de cambios y facilitar la colaboración entre los diferentes integrantes del equipo.

---

# Documentación

La documentación específica de cada tarjeta se encuentra disponible dentro de la carpeta `Docs`.

- `Docs/Nodo/README.md`
- `Docs/Concentrador/README.md`
- `Docs/Concentrador2/README.md`

Cada documento describe detalladamente el proceso de migración, los componentes utilizados, la configuración de bibliotecas, la asignación de códigos LCSC y la generación de los archivos de fabricación correspondientes.

