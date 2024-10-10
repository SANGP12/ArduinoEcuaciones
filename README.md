// Definir variables para los coeficientes y constantes de las ecuaciones 
int n1x, n1y, n1z, n1; 
int n2x, n2y, n2z, n2; 
int n3x, n3y, n3z, n3; 

// Solicitar al usuario que ingrese las ecuaciones en el formato especificado 
Serial.println("Ingrese las ecuaciones en el formato {nx+ny+nz=n}, {nx+ny+nz=n}, {nx+ny+nz=n}"); 

// Leer y almacenar las ecuaciones 
String eq1 = Serial.readStringUntil(','); 
String eq2 = Serial.readStringUntil(','); 
String eq3 = Serial.readStringUntil('}'); 

// Extrae los coeficientes y constantes de las ecuaciones 
n1x = eq1.substring(1,2).toInt(); 
n1y = eq1.substring(3,4).toInt(); 
n1z = eq1.substring(5,6).toInt(); 
n1 = eq1.substring(7,8).toInt(); 

n2x = eq2.substring(1,2).toInt(); 
n2y = eq2.substring(3,4) 
.toInt(); n2z = eq2.substring(5,6).toInt(); 
n2 = eq2.substring(7,8).toInt(); 

n3x = eq3.substring(1,2).toInt(); 
n3y = eq3.substring(3,4).toInt(); 
n3z = eq3.substring(5,6).toInt(); 
n3 = eq3.substring(7,8).toInt(); 

// Crea una matriz para almacenar los coeficientes y constantes 
float matrix[3][4] = { 
  {n1x, n1y, n1z, n1}, 
  {n2x, n2y, n2z, n2}, 
  {n3x, n3y, n3z, n3} 
}; 

// Realiza la eliminación de Gauss-Jordan para resolver el sistema de ecuaciones 
for (int i = 0; i < 3; i++) { 
  // Divide la fila actual por el coeficiente de la variable en la posición pivote 
  float pivot = matrix[i][i]; 
  for (int j = 0; j < 4; j++) { 
    matrix[i][j] = matrix[i][j] / pivot; 
  } 
  // Resta la fila actual de las otras filas para eliminar la variable en la posición pivote 
  for (int k = 0; k < 3; k++) { 
    if (k != i) { 
      float factor = matrix[k][i]; 
      for (int l = 0; l < 4; l++) { 
        matrix[k][l] = matrix[k][l] - factor * matrix[i][l]; 
      } 
    } 
  } 
} 

// Imprime la solución del sistema de ecuaciones 
Serial.print("x = "); 
Serial.println(matrix[0][3]); 
Serial.print("y = "); 
Serial.println(matrix[1][3]); 
Serial.print("z = "); 
Serial.println(matrix[2][3]); 
