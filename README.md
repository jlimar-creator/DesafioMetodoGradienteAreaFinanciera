# Aplicación del Método de Gradientes Conjugados Precondicionado (GCP) en Planificación Financiera y Distribución de Recursos

Plataforma web interactiva para el modelado, análisis de condicionamiento y resolución numérica de sistemas de ecuaciones lineales simétricos y definidos positivos ($Ax = b$, con $n \ge 4$) aplicados a la asignación presupuestaria, flujo de caja interdepartamental y maximización del valor organizacional.

El motor numérico implementa el **Método de Gradientes Conjugados Precondicionado (GCP)** basado en el artículo científico de **Porfirio Suñagua S. (Revista Boliviana de Matemática UMSA, 2020)**, contrastando su precisión y velocidad de convergencia frente al método de Gradientes Conjugados simple (GC) y métodos directos de referencia.

## 1. Ficha Académica del Proyecto

* **Universidad:** Universidad Mayor de San Andrés (UMSA)
* **Facultad:** Facultad de Ciencias Puras y Naturales (FCPN)
* **Carrera:** Informática
* **Asignatura:** Métodos Numéricos
* **Mención Académica:** Ingeniería de Sistemas
* **Estudiante:** Joseph Lima Ramos
* **Modalidad y Área:** Individual • Finanzas
* **Parámetros del Sistema:** $n \ge 4$ ecuaciones ($n = 4$ estándar y $n = 5$ extendido) con tolerancia $\Vert{}r_k\Vert{}_2 / \Vert{}b\Vert{}_2 < 10^{-6}$

## 2. Enlaces de Entrega

* **Página Web Interactiva (GitHub Pages):** `https://TU_USUARIO.github.io/TU_REPOSITORIO/`
* **Repositorio de Código Fuente:** `https://github.com/TU_USUARIO/TU_REPOSITORIO`

## 3. Contexto del Caso Financiero (Mención Ingeniería de Sistemas)

El proyecto modela la planificación financiera anual y la distribución óptima de recursos entre las unidades estratégicas de Tecnologías de Información de la corporación **TechSys Corp S.A.**, cuyas operaciones están acopladas mediante procesos de negocio y Acuerdos de Nivel de Servicio (SLAs) recíprocos. Los montos se expresan en decenas de miles de dólares ($\text{daUSD}$, donde $1\text{ daUSD} = \$10,000\text{ USD}$):

* **$x_1$ ($U_1$):** Presupuesto operativo de la Unidad de Infraestructura Cloud y Data Center.
* **$x_2$ ($U_2$):** Presupuesto operativo de la Unidad de Desarrollo de Software e Ingeniería de Plataformas.
* **$x_3$ ($U_3$):** Presupuesto operativo de la Unidad de Ciberseguridad y Continuidad Operativa (SOC).
* **$x_4$ ($U_4$):** Presupuesto operativo de la Unidad de Analítica Empresarial y Automatización BPM/ERP.
* **$x_5$ ($U_5$):** Presupuesto operativo de la Unidad de Innovación y DevOps (disponible en el modo extendido $n = 5$).

### Formulación Matemática y Reglas de Negocio
El **Valor Organizacional Neto** $V(x)$ se modela mediante la función cuadrática cóncava de utilidad corporativa:

$$V(x) = b^T x - \frac{1}{2} x^T A x$$

Aplicando la condición de primer orden ($\nabla V(x) = b - Ax = 0$), el punto de equilibrio único satisface el sistema lineal $Ax = b$:

* **RN-01 (Absorción Propia Diagonal $a_{ii} > 0$):** Representa el costo marginal de escala y absorción interna de recursos de cada unidad $U_i$.
* **RN-02 (Simetría de Flujo de Caja por SLAs $a_{ij} = a_{ji} \le 0$):** Representa las transferencias recíprocas auditadas por servicios compartidos entre las unidades $U_i$ y $U_j$, asegurando que $A = A^T$.
* **RN-03 (Definición Positiva y Solvencia $x^T A x > 0$):** La absorción interna domina estrictamente las transferencias interdepartamentales, cumpliendo el Criterio de Sylvester ($\Delta_k > 0$) y garantizando autovalores positivos ($\lambda_i > 0$).
* **RN-04 (Consistencia entre Escenarios):** Los escenarios mantienen la estructura organizacional modificando de forma fundamentada las tasas de absorción en $A$ y las metas de liquidez en $b$.

## 4. Arquitectura del Sistema

La aplicación está diseñada bajo una arquitectura **Single-Page Application (SPA)** reactiva ejecutada íntegramente en el navegador del cliente (Client-Side Rendering), estructurada en tres capas principales:

### 4.1. Estructura de Archivos del Repositorio

```text
├── index.html                                    # Interfaz interactiva (10 módulos) y motor numérico ES6+
├── docs/
│   └── Desafio_Gradientes_Conjugados_Finanzas.pdf 
└── README.md                                     # Documentación de arquitectura, instalación y uso local
