# Trabajo Git
### 1.Expectativas antes de aprender POO:
![](img.png)

**Que creía que iba a aprender y para que me iba a servir:**
  - A crear entidades que sirviesen para dividir el programa en partes más pequeñas que juntas pudiesen hacer el programa entero
  - Estos objetos podrían ser reutilizados en otros programas en caso de necesitarlos
  - Cada objeto tendría acceso a sus propios datos y así no molestarían a otras entidades del programa a no ser que nosotros lo quisieramos

### 2.Que he aprendido durante estas unidades:
[Haz click aquí para conocer más sobre la POO](https://jorgesanchez.net/manuales/viejos/fpr/fpr0609.pdf)
- [x] A diferenciar entre clase y objeto 
- [x] A programar con objetos
- [x] A crear constructores
- [x] A comprender las diferencias entre private,friendly,protected y public 
- [x] La diferencia entre subclase y superclase
- [x] Como funciona la herencia entre clases
- [x] A sobrescribir con Override
- [x] A comprender y diseñar diagramas y esquemas UML
  [10:50] MARIO PERNÍA VICENTE
### 3.Dos ejercicios de las prácticas:
* **Ejercicio1:**

1.  *Clase Punto:*
````
    public class Punto {
    private double x;
    private double y;
    public double getX() {
        return x;
    }
    public double getY() {
        return y;
    }
    public void setX(double x) {
        this.x = x;
    }
    public void setY(double y) {
        this.y = y;
    }
    public void cambiarCoords(double x, double y){
        this.x = x;
        this.y = y;
    }
    public Punto copia(){
        Punto p = new Punto();
        p.cambiarCoords(x, y);
        return p;
    }
    public boolean iguales(Punto p){
        return x == p.x && y == p.y;
    }
    public void sumaCoords(Punto p){
        x += p.x;
        y += p.y;
    }
    public double obtenerDistancia(Punto p){
        double dx = x - p.x;
        double dy = y - p.y;
        return Math.sqrt(dx*dx + dy*dy);
    }
    public class Rectangulo {
    private Punto esquina;
    private double anchura;
    private double altura;
    public void setAnchura(double anchura) {
        this.anchura = anchura;
    }
    public void setAltura(double altura) {
        this.altura = altura;
    }
    public void cambiarEsquina(double x, double y){
            esquina.cambiarCoords(x, y);
        }
    public void cambiarEsquina(Punto p){
        esquina = p;
    }
    public void dibujar(){
       for(int i=1; i<=altura; i++){
           for(int j=1; j<=anchura; j++){
               System.out.print("*");
           }
           System.out.println();
       }
    }
    
````
2. *Clase Rectangulo:*
````
    public class Rectangulo {
    private Punto esquina;
    private double anchura;
    private double altura;
    public void setAnchura(double anchura) {
        this.anchura = anchura;
    }
    public void setAltura(double altura) {
        this.altura = altura;
    }
    public void cambiarEsquina(double x, double y){
            esquina.cambiarCoords(x, y);
        }
    public void cambiarEsquina(Punto p){
        esquina = p;
    }
    public void dibujar(){
       for(int i=1; i<=altura; i++){
           for(int j=1; j<=anchura; j++){
               System.out.print("*");
           }
           System.out.println();
       }
    }
    public void dibujar(char c){
         for(int i=1; i<=altura; i++){
              for(int j=1; j<=anchura; j++){
                System.out.print(c);
              }
              System.out.println();
         }
    }
    public boolean interior(Punto p){
        return p.getX() >= esquina.getX() &&
               p.getX() <= esquina.getX() + anchura &&
               p.getY() >= esquina.getY() &&
                p.getY() <= esquina.getY() + altura;
    }
    public Punto[] vertices(){
        Punto[] p = new Punto[4];
        p[0] = esquina.copia();
        p[1] = new Punto();
        p[1].cambiarCoords(esquina.getX() + anchura, esquina.getY());
        p[2] = new Punto();
        p[2].cambiarCoords(esquina.getX() + anchura, esquina.getY() + altura);
        p[3] = new Punto();
        p[3].cambiarCoords(esquina.getX(), esquina.getY() + altura);
        return p;
    }
}
````
| Importancia                                                                                        | ¿Como lo he resuelto?                                       | ¿Que he aprendido?                                                              |
|----------------------------------------------------------------------------------------------------|-------------------------------------------------------------|---------------------------------------------------------------------------------|
| Es el primer ejercicio que hicimos y ayuda a comprender las utilidades de las clases y los objetos | Utilizando el punto como una esquina para crear rectángulos | La utilidad de conectar una clase con otra (utilizar el punto en el rectángulo) |

* **Ejercicio2:**

1.  *Clase carta:*
````
public class Carta {
    private int palo;
    private int valor;
    private static final int OROS=1;
    private static final int ESPADAS=2;
    private static final int BASTOS=3;
    private static final int COPAS=4;
    private static final int AS=1;
    private static final int SOTA=8;
    private static final int CABALLO=9;
    private static final int REY=10;
    private static final String[] PALOS = {"","Oros","Espadas","Bastos","Copas"};
    private static final String[] VALORES = {"","As","2","3","4","5","6","7","Sota","Caballo","Rey"};
    public Carta(int palo, int valor) {
        darValor(palo,valor);
    }
    public Carta(){
        darValor(Carta.OROS, Carta.AS);
    }
    public void darValor(int palo,int valor){
        this.valor = valor;
        this.palo = palo;
    }
    public void escribe(){
        System.out.println(VALORES[valor]+" de "+PALOS[palo]);
    }
}
````
2. *Clase baraja:*
````
public class Baraja {
    private Carta[] cartas;
    private int numCartas;
    private static final int NUM_PALOS = 4;
    private static final int NUM_CARTAS = 10;
    public Baraja() {
        cartas = new Carta[NUM_PALOS * NUM_CARTAS];
        numCartas = 0;
        for (int palo = 1; palo <= NUM_PALOS; palo++) {
            for (int valor = 1; valor <= NUM_CARTAS; valor++) {
                cartas[numCartas] = new Carta(palo, valor);
                numCartas++;
            }
        }
    }
    public void barajar() {
        for (int i = 0; i < 100; i++) {
            int pos1 = (int) (Math.random() * numCartas);
            int pos2 = (int) (Math.random() * numCartas);
            Carta aux = cartas[pos1];
            cartas[pos1] = cartas[pos2];
            cartas[pos2] = aux;
        }
    }

    public void escribe() {
        for (int i = 0; i < numCartas; i++) {
            cartas[i].escribe();
        }
    }
}
````
| Importancia                                                                                                   | ¿Como lo he resuelto?                                                     | ¿Que he aprendido?                  |
|---------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------|
| Es el primer ejercicio en el que introducimos una cantidad de objetos en otra clase (cartas dentro de baraja) | Creando un array de objetos carta llamado "cartas" que conforma la baraja | A manejar y crear arrays de objetos |
>Si bien es verdad que puede que estos ejercicios no sean los mas complicados en comparación a los que hemos hecho después, son los primeros que sirven para asentar las bases y ver nuevo contenido por lo cual los considero esenciales.