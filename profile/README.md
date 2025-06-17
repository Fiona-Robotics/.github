# 📄 Guía de Buenas Prácticas para Pull Requests (PRs)
---

## 🎯 Objetivo

Evitar conflictos de código, pérdida de avances y errores no detectados en pruebas mediante un flujo claro y ordenado de trabajo con Pull Requests (PRs), especialmente en entornos que incluyen hardware y pruebas físicas.

---

## 1. 📌 Un PR = Una funcionalidad

- Cada PR debe enfocarse en **una sola tarea** (feature, fix, refactor, etc.).
- Si en el desarrollo surge algo no planificado, **crear un nuevo branch** y PR separado.
- Evitar grandes PR con múltiples propósitos.

---

## 2. 🧱 Aislamiento y orden de trabajo

- Crear un branch nuevo desde `develop` o `main` (según política del repo).
- Usar nombres descriptivos:  
  `feature/deteccion-sensor`, `fix/bug-led`, `refactor/handler-uart`
- Antes de comenzar, **sincroniza tu branch con la rama base actualizada**.

---

## 3. 📣 Declarar clases y archivos a modificar

Antes de comenzar o al abrir el PR, **indicar qué clases o archivos se planea tocar**:

```markdown
🔧 Archivos/clases afectados:
- `SensorManager`
- `config/hardware_map.yaml`
```

- Si otro miembro está trabajando en alguno de ellos, **coordinarlo antes de hacer cambios**.
- Si no hay respuesta en 24 horas, comentar el PR con:  
  `@persona Estoy modificando temporalmente esta clase por necesidad de la tarea. Coordinemos si hay solapamiento.`
- Considerar extender, copiar temporalmente o inyectar dependencias si es una clase crítica.

---

## 4. 💻 Pruebas cruzadas en hardware

- Todo cambio debe probarse **en al menos dos estaciones/hardware distintos** antes de hacer merge.
- Documentar en el PR dónde se probó:

```markdown
🧪 Pruebas realizadas:
✔ Estación 1 (Jose-PC): Sensor responde correctamente
✔ Estación 3 (Lab-Taller): LEDs funcionan
✘ Estación 2: No conecta por error en puerto (investigando)
```

- Si no es posible probar en dos, indicar razones justificadas.

---

## 5. 📥 Revisión obligatoria

- Ningún PR puede ser mergeado sin revisión de otro miembro del equipo.
- El revisor debe:
  - Leer los cambios
  - Probar (idealmente en otra estación)
  - Confirmar que se respeta este protocolo

---

## 6. 🔒 No tocar código ajeno sin avisar

- No modificar archivos/clases que no son parte de tu tarea sin anunciarlo en el PR.
- Si es un bug urgente fuera de tu scope, **crear un issue o PR específico**.
- Comentar explícitamente en el PR si se tocó algo fuera del alcance:

```markdown
⚠ Cambios extra:
- Se corrigió error en `LEDController` que bloqueaba lectura del sensor. Confirmado con @Patricio.
```

---

## 7. 💬 Estructura de PR esperada

Cada PR debe incluir:

- ✅ Descripción clara de la tarea realizada
- 📂 Lista de archivos/clases modificados
- 🧪 Pruebas realizadas (estaciones y resultados)
- 📌 Consideraciones especiales (dependencias, conflictos, limitaciones)

Ejemplo:

```markdown
### Descripción
Se implementa la lectura de temperatura con calibración personalizada para la sonda DS18B20.

### Archivos afectados
- `TemperatureReader.cpp`
- `calibration_config.json`

### Pruebas
✔ Probado en Estación 1 y 3  
✘ Estación 2 aún sin hardware

### Consideraciones
- Coordinado con @Mauricio que no hará cambios en `TemperatureReader.cpp` esta semana.
```

---

## 8. 🚫 Errores comunes a evitar

- Trabajar sin branch dedicado
- Probar solo en tu PC
- Tocar clases críticas sin avisar
- Mergear sin revisión
- Hacer commits grandes sin separar funcionalidad
- No indicar qué fue probado y dónde

---

## 9. 🧪 PR como punto de inicio (Draft PR)

- Al comenzar una nueva funcionalidad, se recomienda **crear una Pull Request en estado _Draft_**.
- Esto permite a todo el equipo saber qué estás desarrollando, qué clases/módulos tocarás y si hay solapamientos.
- Actualiza el PR con tus avances a medida que trabajas.
- Cuando esté listo, **marca el PR como “Ready for Review”** y avisa al equipo.
