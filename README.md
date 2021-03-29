# prestamos-enisa
# **UOC - Tipologia y Ciclo de vida de los datos**
*Victor María Cardoner Alvarez*

*Jose Oriol Bielsa Nogaledo*

## **1. Contexto**

El objetivo de este proyecto es analizar la evolución de la empresas a las que **Enisa**, entidad pública dependiente del Ministerio de Industria, Comercio y Turismo, concede **financiación para impulsar su actividad emprendedora**. 

Los préstamos se organizan en diferentes líneas en función de la madurez de la empresa, por importes de entre 25.000€ y 1.5M€ y plazos hasta 9 años. Estos préstamos tienen además otras ventajas que los hacen muy interesantes para empresas en sus etapas iniciales, como la carencia hasta 7 años, la posibilidad de deducir los intereses del impuesto de sociedades, la remuneración en funcion de los resultados o que no requieren garantías ni avales.

## **2. Título del dataset**

Hemos decidido denominar este dataset como **prestamos-enisa**.

## **3. Descripción del dataset**

TBD

## **4. Representación gráfica del dataset**

TBD

## **5. Contenido**

**(1) ENISA**

La base de datos de Enisa contiene todo el histórico de préstamos concedidos desde 2005 y se pueden consultar en la página https://www.enisa.es/es/comunidad-enisa/prestamos. En la actualidad constan 7063 préstamos concedidos etiquetados con los siguientes campos: **Razón Social, Marca comercial, Importe, Fecha, Comunidad Autónoma y Provincia**. Este listado se puede obtener haciendo scraping directo, y va a ser el core de datos sobre el que vamos a trabajar y enriquecer.

Una vez obtenidos estos datos, se pueden enriquecer con plataformas de datos mercantiles como Infocif.es, Axesor.es e Informa.es. El objetivo inicial es añadir el CIF de la empresa para una búsqueda más sencilla de otros datos como página web, dirección, código de actividad CNAE y otros datos financieros.
Posteriormente, también planteamos enriquecer con datos más de ámbito de RRSS como podría ser Linkedin o Twitter.

**(2) INFOCIF, AXESOR e INFORMA.ES**

Usando **Infocif** podemos recuperar unos 5000 **CIFs** del total de los préstamos. Con el CIF se puede recuperar información en Axesor e Informa usando Selenium y BeautifulSoup, aunque su fichero robots.txt desincentiva su uso vía scraping (son plataformas de pago con API propia pero con límite de consultas tanto en la versiones gratis como de pago). La idea es hacer una extracción de un número bajo de CIFs como muestra de la oprativa, pero no extraer los 5000 datapoints para no incumplir las recomendaciones del fichero robots.
Como la información presente en informa y Axesor es similar, de hecho son competencia, hemos escogido Axesor por simplicidad. Usando Selenium, generamos la URL estática de cada empresa con la que, posteriormente, usando BeautifulSoup, extraeremos 4 campos: **dirección completa, fecha de constitución de la empresa, CNAE y SIC**. Estos dos últimos campos se refieren al sector de actividad de la empresa.

**(3) TWITTER y LINKEDIN**

Para poder continuar con el estudio, el objetivo es analizar la actividad de LinkedIn y Twitter como indicadores de salud de la empresa. 

En **Linkedin** hacemos scraping usando Selenium, lanzando consultas directamente desde su buscador usando el campo Marca Comercial extraído de Enisa. De esta manera, planteamos extraer la siguiente información de la empresa: **web, sector, tamaño, sede y tipo**.

Por otra parte, para **Twitter** usamos la librería snsscrape -evitando el uso de la API-. En esta plataforma hemos identificado dos vías para la explotación de datos: o bien fuerza bruta -relacionando la Marca Comercial con el handle de Twitter-, o bien buscando por el hashtag #clienteEnisa -usada por la propia Enisa para hacer difusión de las empresas a las que concede préstamos-. El objetivo final es extraer un indicador básico de presencia o actividad en redes: número de **menciones en tweets en los últimos 90 días**.

## **6. Agradecimientos**

TBD

## **7. Inspiración**

En ausencia de un grupo de control con empresas similares pero sin este tipo de financiación, hemos considerado diferentes **estudios que miden la mortalidad de las startups en sus etapas inciales** para comparar estas métricas con las observadas entre los receptores de los préstamos Enisa.

Un estudio ya clásico encabezado por investigadores de las Universidades de Berkeley y Stanford que analizó más de 3200 start-ups, el Startup Genome Project, cifraba la tasa de fracaso de estas empresas en la cota del 90%, y en el caso del 10% que sí tenían éxito también sufrían experiencias de crisis graves que las expusieron a la desaparición. Estos datos han venido siendo confirmados, con leves diferencias estadísticas, por análisis posteriores de Bloomberg, Forbes o Kaufman Foundation.

Este dataset pretende ser una **herramienta que permita de trabajo y control para mitigar estos problemas** comentados. Entendemos que con la información que proporciona, se podrían generar diversas métricas o indicadores que permitieran hacer un seguimiento activo de estas empresas, pudiendo estudiar la viabilidad y evolución de estas.

## **8. Licencia**

TBD

## **9. Código**

Por el momento estamos trabajando en notebooks "por separado" para el scraping de cada fuente de datos. Queda pendiente unir la información, y estructurar proyecto en PyCharm.

## **10. Dataset**

En el GitHub presentamos CSVs de ejemplo de datos obtenidos para cada fuente de datos.
