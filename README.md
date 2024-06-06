# Data-structures-proyect
Data structures proyect

required application: Aplicación requerida por lo que es importante intalar antes de ejecutar
  -windows_10_cmake_Release_graphviz-install-11.0.0-win64.exe
  
adjancency_Matrix: Archivo de texto que el profe nos suminsitro para el ejercicio con lo grafos
  -matriz_de_adyacencias_30x30.txt
  
src: Codigo c++ del proyeto 
  -Main.cpp
  
images: Donde se almacenarán las imagenes generados de los arboles binarios

Data structures proyect.dev  // proyecto para abrir con aplicación c++

Data structures proyect.exe // Permite ejecutar el software sin tener instalado copilador C++

************************************************************************************************

Esto es para editar



1. Debe tener un menú principal en donde se pueda escoger 2 opciones.

1.1.  Presentar ABB Autobalanceados.

1.2.  Presentar Grafos.

2. Cada opción del menú principal debe permitir lo siguiente:

2.1. El submenú para árboles tiene las siguientes opciones: 
            a. Ingrese la lista de nodos y el recorrido para construir el árbol.
            b. Mostrar de forma visual el árbol inicial (indica si el árbol es AVL o no).
            c. Convertir en  AVL (si es el caso) el árbol inicial y mostrar la visualización del árbol.
            d. Convertir en arbol Rojo y Negro el arbol inicial y mostrar la visualización del árbol.

2.2. el submenú para grafos debe llevar las siguientes opciones:
            a. Ingrese la matriz de adyacencias (debe leer si es un grafo dirigido ponderado o un grafo no dirigido ponderado) para construir el grafo.
            b. Mostrar la visualización del grafo inicial.
            c. Entra a un submenú (Elija un algoritmo para encontrar el camino más corto)
                                                  -  Dijkstra (utiliza el grafo inicial resuelve con el algoritmo y luego entrega la solución)
                                                  -  Floyd-Warshall (utiliza el grafo inicial resuelve con el algoritmo y luego entrega la solución)
            d. Entra a un submenú (Elija un algoritmo para encontrar árboles de peso mínimo)
                                                  - Kruskal (utiliza el grafo inicial resuelve con el algoritmo y luego entrega la solución)
                                                  - Prim (utiliza el grafo inicial resuelve con el algoritmo y luego entrega la solución)
3. debe tener la opción de retornar al menú después de mostrar el resultado.

4. el código debe estar subido a github y en el readme una explicación con gráficos de ejemplo de cada opción.



---------------------------------------------------------------------------------------------------------------------------------------------------------------

## // PARTE DE GRAFOS -------------------------------------------------------------------------------------------------------------------------

### // Estructura para representar un grafo

  **Estructura `Graph`:** Esta estructura representa un grafo. Dentro de esta estructura, se utiliza un `vector` de `vector`s de enteros (`vector<vector<int>>`) llamado `adjacencyMatrix`. 
  Este es un método común para representar grafos, donde cada fila y columna corresponden a un nodo del grafo, y el valor en la intersección indica si hay una arista entre esos dos nodos o cuál es su peso (si existe). 
  Un valor de 0 generalmente significa que no hay arista entre los nodos correspondientes.

```C++
// Estructura para representar un grafo
  struct Graph {
      vector<vector<int>> adjacencyMatrix;
  };
```

### // Estructura para representar una arista
  
  **Estructura `Edge`:** Esta estructura representa una arista en el grafo. Contiene tres miembros:
  **`src`:** Representa el nodo origen de la arista.
  **`dest`:** Representa el nodo destino de la arista.
  **`weight`:** Representa el peso de la arista, que puede ser utilizado para representar, por ejemplo, la distancia entre los nodos si el grafo representa una red de caminos o una red social.

```C++
// Estructura para representar una arista  
struct Edge {
    int src, dest, weight;
};
```
### // Función para imprimir la matriz de adyacencia

  La función printAdjacencyMatrix está diseñada para imprimir la matriz de adyacencia de un grafo. La matriz de adyacencia es una representación común de grafos en programación,
  donde cada fila y columna representan un nodo del grafo, y el valor en la intersección indica si hay una arista entre esos dos nodos o cuál es su peso.

  **Parámetro `matrix`:** La función recibe una referencia constante a un `vector` de `vector`s de enteros (`vector<vector<int>>`). Este parámetro representa la matriz de adyacencia del grafo.
  
  **Bucle externo:** El primer bucle `for` itera sobre cada fila de la matriz de adyacencia. Esto se logra utilizando un rango basado en `auto`,
  lo que permite iterar sobre cada fila sin necesidad de especificar explícitamente el tipo de dato.
 ** Bucle interno:** Dentro del bucle externo, hay otro bucle `for` que itera sobre cada elemento (valor) de la fila actual. Este bucle utiliza la sintaxis moderna de rango para iterar sobre todos los elementos de la fila.
  
  **Impresión de valores:** Para cada valor en la fila, se imprime el valor seguido de un espacio. Esto se hace usando `cout`, que es la salida estándar en C++.
  Al final de cada fila, se imprime un salto de línea (`endl`) para comenzar una nueva fila en la salida.

```C++
  // Función para imprimir la matriz de adyacencia
void printAdjacencyMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) { // Itera sobre cada fila de la matriz
        for (int value : row) { // Itera sobre cada elemento de la fila actual
            cout << value << " "; // Imprime el valor del elemento
        }
        cout << endl; // Cambia de línea después de imprimir toda la fila
    }
}
```

### // Función para leer la matriz de adyacencia desde un archivo de texto

  La función `readAdjacencyMatrixFromFile` tiene como objetivo leer una matriz de adyacencia desde un archivo de texto y devolverla como un `vector` de `vectors` de enteros. 
  Esta función es especialmente útil cuando se trabaja con gráficos y se necesita cargar datos de un archivo para realizar análisis o manipulaciones.

  **Parámetro `filename`:** La función acepta un `string` que representa el nombre del archivo desde el cual se leerá la matriz de adyacencia.
  
  **Inicialización de la matriz:** Se inicializa un `vector` de `vector`s de enteros (`vector<vector<int>>`) vacío llamado `matrix` para almacenar la matriz de adyacencia leída del archivo.
  
  **Apertura del archivo :** Se intenta abrir el archivo con el nombre proporcionado. Si el archivo se abre correctamente, se procede a leerlo; De lo contrario, se informa de un error.
  
  **Lectura del archivo :** See lee el archivo línea por línea. Cada línea se procesa mediante un `stringstream` para convertirla en un formato que pueda ser fácilmente analizado.
  
  **Análisis de líneas y filas :** Cada línea se divide en valores separados por comas, que se agregan a un `vector` de enteros (`row`).
  Después de procesar todos los valores de una línea, esa fila se agrega a la matriz principal.
  
  **Cierre del archivo :** Una vez que se hayan leído todas las líneas del archivo, se cierra el archivo.
  
  **Retorno de la matriz :** Finalmente, la función devuelve la matriz de adyacencia leída del archivo.

  ```c++
  // Función para leer la matriz de adyacencia desde un archivo de texto
vector<vector<int>> readAdjacencyMatrixFromFile(const string& filename) {
    vector<vector<int>> matrix; // Vector vacío para almacenar la matriz de adyacencia
    ifstream file(filename); // Intenta abrir el archivo con el nombre dado
    if (file.is_open()) { // Verifica si el archivo se abrió correctamente
        string line; // Variable temporal para almacenar cada línea del archivo
        while (getline(file, line)) { // Lee cada línea del archivo
            stringstream ss(line); // Convierte la línea leída en un stream de entrada
            vector<int> row; // Vector para almacenar los valores de una fila
            int value; // Variable temporal para almacenar cada valor leído
            while (ss >> value) { // Extrae valores del stream hasta que no haya más
                row.push_back(value); // Agrega el valor extraído al vector de la fila
                if (ss.peek() == ',') // Comprueba si el siguiente carácter es una coma
                    ss.ignore(); // Ignora el carácter de coma si está presente
            }
            matrix.push_back(row); // Agrega la fila completa al vector de la matriz
        }
        file.close(); // Cierra el archivo después de leerlo completamente
    } else {
        cerr << "Error: No se pudo abrir el archivo." << endl; // Informa de error si el archivo no se pudo abrir
    }
    return matrix; // Devuelve la matriz de adyacencia leída
}
```
### // Función para leer el grafo desde un archivo de texto

Esta documentación proporciona una visión general de lo que hace la función, describe el parámetro de entrada (`filename`), y explica lo que la función devuelve (`un objeto Graph`). 
También menciona brevemente la expectativa sobre el formato del archivo de texto, aunque esto último dependería de la implementación específica de `readAdjacencyMatrixFromFile`

 ```c++
// Función para leer el grafo desde un archivo de texto
Graph readGraphFromFile(const string& filename) { //Nombre del archivo de texto que contiene la información del grafo.
    Graph graph;
    graph.adjacencyMatrix = readAdjacencyMatrixFromFile(filename);
    return graph; //Un objeto Graph que contiene la matriz de adyacencia del grafo leído.
}
 ```

### // Función para generar y guardar un archivo DOT para un grafo

La función `generateDotFile` que tiene como objetivo generar un archivo DOT para un grafo dado. Los archivos DOT son utilizados por herramientas como Graphviz para visualizar grafos. A continuación, se detalla el funcionamiento de esta función con comentarios explicativos:

```c++
// Función para generar y guardar un archivo DOT para un grafo
void generateDotFile(const Graph& graph, const string& filename) {
    ofstream dotFile(filename); // Intenta abrir el archivo con el nombre dado para escritura
    if (dotFile.is_open()) { // Verifica si el archivo se abrió correctamente
        dotFile << "graph G {" << endl; // Comienza la definición del grafo en el formato DOT
        for (int i = 0; i < graph.adjacencyMatrix.size(); ++i) { // Itera sobre cada nodo del grafo
            for (int j = i + 1; j < graph.adjacencyMatrix.size(); ++j) { // Itera sobre los posibles pares de nodos conectados
                if (graph.adjacencyMatrix[i][j]!= 0) { // Verifica si hay una arista entre los nodos i y j
                    dotFile << i << " -- " << j << " [label=\"" << graph.adjacencyMatrix[i][j] << "\"];" << endl; // Agrega la arista al archivo DOT
                }
            }
        }
        dotFile << "}" << endl; // Cierra la definición del grafo
        dotFile.close(); // Cierra el archivo
        cout << "Archivo DOT generado: " << filename << endl; // Informa que el archivo DOT fue generado exitosamente
    } else {
        cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl; // Maneja el caso en que el archivo no se pudo abrir
    }
}
```

**Parámetros**:
  `graph`: Una referencia constante al objeto `Graph` que representa el grafo cuyo archivo DOT se va a generar.
  `filename`: Una cadena que contiene el nombre del archivo DOT que se generará.

 **Proceso**:
  1. Se intenta abrir un archivo con el nombre especificado en el parámetro `filename` para escritura.
  2. Si el archivo se abre correctamente, se inicia la definición del grafo en el formato DOT con `"graph G {"`.
  3. Luego, se itera sobre cada posible par de nodos en el grafo. Para cada par de nodos `(i, j)` donde `i < j`, se verifica si hay una arista entre ellos mediante el valor en la posición `[i][j]` de la matriz de adyacencia del grafo.
  4. Si existe una arista (es decir, el valor no es 0), se agrega una línea al archivo DOT que representa esta arista, incluyendo el peso de la arista como etiqueta.
  5. Después de procesar todas las aristas, se cierra la definición del grafo con `"}` y se cierra el archivo.
  6. Finalmente, se informa que el archivo DOT fue generado exitosamente.

 **Manejo de errores**:
  Si el archivo no se pudo abrir para escritura, se emite un mensaje de error indicando que no se pudo abrir el archivo DOT para escribir.

Esta función es útil para generar archivos DOT de grafos, permitiendo su posterior visualización con herramientas como Graphviz, lo cual es invaluable para analizar y entender la estructura de los grafos.

###// Algoritmo de Floyd-Warshall para encontrar todas las distancias más cortas entre todos los pares de vértices

El código proporcionado implementa el algoritmo de Floyd-Warshall para calcular todas las distancias más cortas entre todos los pares de vértices en un grafo. Además, genera un archivo DOT para visualizar el resultado y, opcionalmente, una imagen PNG de ese grafo. A continuación, se detalla el funcionamiento de esta función con comentarios explicativos:

```c++
// Algoritmo de Floyd-Warshall para encontrar todas las distancias más cortas entre todos los pares de vértices
void floydWarshall(const Graph& graph) {
    int V = graph.adjacencyMatrix.size(); // Obtiene el número de vértices en el grafo
    vector<vector<int>> dist(V, vector<int>(V, numeric_limits<int>::max())); // Inicializa la matriz de distancias con infinito

    // Inicializar la matriz de distancias con los pesos de las aristas
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            dist[i][j] = graph.adjacencyMatrix[i][j]; // Copia los pesos directos de las aristas
        }
    }

    // Actualizar las distancias mínimas entre todos los pares de vértices
    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][k]!= numeric_limits<int>::max() && dist[k][j]!= numeric_limits<int>::max() &&
                    dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j]; // Actualiza la distancia mínima si es menor
                }
            }
        }
    }

    // Imprimir las distancias mínimas entre todos los pares de vértices
    cout << "Distancias mínimas entre todos los pares de vértices (Floyd-Warshall):" << endl;
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            if (dist[i][j] == numeric_limits<int>::max())
                cout << "INF "; // Imprime INF si la distancia es infinita
            else
                cout << dist[i][j] << " "; // Imprime la distancia si no es infinita
        }
        cout << endl;
    }

    // Generar archivo DOT para visualizar el resultado de Floyd-Warshall
    ofstream dotFile("floyd_warshall.dot"); // Intenta abrir el archivo DOT para escritura
    if (dotFile.is_open()) {
        dotFile << "graph G {" << endl; // Comienza la definición del grafo en el formato DOT
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][j]!= numeric_limits<int>::max() && i!= j) { // Solo dibuja aristas no nulas
                    dotFile << i << " -- " << j << " [label=\"" << dist[i][j] << "\"];" << endl; // Dibuja la arista con su peso
                }
            }
        }
        dotFile << "}" << endl; // Cierra la definición del grafo
        dotFile.close(); // Cierra el archivo
        cout << "Archivo DOT generado para Floyd-Warshall: floyd_warshall.dot" << endl;

        // Verificar si el archivo DOT se ha generado correctamente
        ifstream checkFile("floyd_warshall.dot");
        if (checkFile.is_open()) {
            checkFile.close();
            // Generar la imagen PNG a partir del archivo DOT
            if (system("dot -Tpng floyd_warshall.dot -o floyd_warshall.png") == 0) {
                cout << "Imagen de Floyd-Warshall generada como 'floyd_warshall.png'." << endl;
            } else {
                cerr << "Error: No se pudo generar la imagen de Floyd-Warshall." << endl;
            }
        } else {
            cerr << "Error: El archivo DOT de Floyd-Warshall no se generó correctamente." << endl;
        }
    } else {
        cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl;
    }
}
```
Este función realiza lo siguiente:

1. **Inicialización**: Calcula el número de vértices en el grafo y crea una matriz de distancias inicializada con infinito (usando `numeric_limits<int>::max()`).

2. **Carga de pesos de aristas**: Copia los pesos de las aristas directas de la matriz de adyacencia del grafo a la matriz de distancias.

3. **Actualización de distancias**: Aplica el algoritmo de Floyd-Warshall para actualizar las distancias mínimas entre todos los pares de vértices.

4. **Impresión de resultados**: Imprime las distancias mínimas calculadas.

5. **Generación de archivo DOT**: Crea un archivo DOT que representa el grafo con las distancias mínimas encontradas.

6. **Generación de imagen PNG**: Utiliza Graphviz para generar una imagen PNG del grafo a partir del archivo DOT creado.

Este proceso permite visualizar gráficamente el grafo con las distancias mínimas calculadas por el algoritmo de Floyd-Warshall, facilitando la comprensión de la estructura del grafo y las relaciones entre sus vértices.


###// Función para el algoritmo de Dijkstra

Se implementa el algoritmo de Dijkstra para encontrar las distancias mínimas desde un nodo inicial a todos los demás nodos en un grafo. 
Además, genera un archivo DOT para visualizar el resultado y, opcionalmente, una imagen PNG de ese grafo.

```c++
// Función para el algoritmo de Dijkstra
void dijkstra(const Graph& graph, int startNode) {
    int numNodes = graph.adjacencyMatrix.size(); // Obtiene el número total de nodos en el grafo
    vector<int> dist(numNodes, numeric_limits<int>::max()); // Inicializa la matriz de distancias con infinito
    vector<bool> visited(numNodes, false); // Vector para marcar los nodos visitados

    dist[startNode] = 0; // La distancia desde el nodo inicial hasta sí mismo es 0

    for (int count = 0; count < numNodes - 1; ++count) { // Itera hasta menos uno porque el nodo inicial ya está marcado
        int minDist = numeric_limits<int>::max(); // Busca el nodo con la distancia mínima no visitada
        int minIndex = -1;

        // Encuentra el nodo no visitado con la distancia mínima
        for (int i = 0; i < numNodes; ++i) {
            if (!visited[i] && dist[i] < minDist) {
                minDist = dist[i];
                minIndex = i;
            }
        }

        if (minIndex == -1) // Si no se encuentra ningún nodo no visitado, termina el algoritmo
            break;

        visited[minIndex] = true; // Marca el nodo encontrado como visitado

        // Actualiza las distancias de los nodos adyacentes al nodo seleccionado
        for (int i = 0; i < numNodes; ++i) {
            if (!visited[i] && graph.adjacencyMatrix[minIndex][i] && // Verifica si hay una arista y si el nodo no visitado
                dist[minIndex]!= numeric_limits<int>::max() && // Evita comparaciones con infinito
                dist[minIndex] + graph.adjacencyMatrix[minIndex][i] < dist[i]) { // Actualiza la distancia si es menor
                dist[i] = dist[minIndex] + graph.adjacencyMatrix[minIndex][i];
            }
        }
    }

    // Imprime las distancias mínimas desde el nodo inicial
    cout << "Distancias mínimas desde el nodo " << startNode << " (Dijkstra):" << endl;
    for (int i = 0; i < numNodes; ++i) {
        cout << "Nodo " << i << ": " << dist[i] << endl;
    }

    // Genera archivo DOT para visualizar el resultado de Dijkstra
    ofstream dotFile("dijkstra.dot"); // Intenta abrir el archivo DOT para escritura
    if (dotFile.is_open()) {
        dotFile << "graph G {" << endl; // Comienza la definición del grafo en el formato DOT
        for (int i = 0; i < numNodes; ++i) {
            if (dist[i]!= numeric_limits<int>::max() && i!= startNode) { // Solo dibuja aristas no nulas
                dotFile << startNode << " -- " << i << " [label=\"" << dist[i] << "\"];" << endl; // Dibuja la arista con su peso
            }
        }
        dotFile << "}" << endl; // Cierra la definición del grafo
        dotFile.close(); // Cierra el archivo
        cout << "Archivo DOT generado para Dijkstra: dijkstra.dot" << endl;

        // Verifica si el archivo DOT se ha generado correctamente
        ifstream checkFile("dijkstra.dot");
        if (checkFile.is_open()) {
            checkFile.close();
            // Genera la imagen PNG a partir del archivo DOT
            if (system("dot -Tpng dijkstra.dot -o dijkstra.png") == 0) {
                cout << "Imagen de Dijkstra generada como 'dijkstra.png'." << endl;
            } else {
                cerr << "Error: No se pudo generar la imagen de Dijkstra." << endl;
            }
        } else {
            cerr << "Error: El archivo DOT de Dijkstra no se generó correctamente." << endl;
        }
    } else {
        cerr << "Error: No se pudo abrir el archivo DOT para escribir." << endl;
    }
}
```

Este código realiza lo siguiente:

1. **Inicialización**: Prepara los vectores `dist` y `visited` para almacenar las distancias mínimas desde el nodo inicial a todos los demás nodos y marcar los nodos visitados, respectivamente.

2. **Ejecución del algoritmo de Dijkstra**: Implementa el algoritmo de Dijkstra para encontrar las distancias mínimas desde el nodo inicial a todos los demás nodos en el grafo.

3. **Impresión de resultados**: Imprime las distancias mínimas desde el nodo inicial a todos los demás nodos.

4. **Generación de archivo DOT**: Crea un archivo DOT que representa el grafo con las distancias mínimas encontradas por el algoritmo de Dijkstra.

5. **Generación de imagen PNG**: Utiliza Graphviz para generar una imagen PNG del grafo a partir del archivo DOT creado.

Este proceso permite visualizar gráficamente el grafo con las distancias mínimas calculadas por el algoritmo de Dijkstra, facilitando la comprensión de la estructura del grafo y las relaciones entre sus vértices.
