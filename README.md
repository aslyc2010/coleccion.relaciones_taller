# coleccion.relaciones_taller

necesito que cambies todo esto y que quede distinto pero que n o deje de funcionar igual mente
# colecciones_relacoiones

public class PruebaLista {
    private static void main(String[] args) {
        ArrayList<String> generos = new ArrayList<>();

        generos.add("Rock");
        generos.add("Salsa");
        generos.add("Vallenato");

        System.out.println(generos.size());
        System.out.println(generos.get(1));

        generos.set(1, "Merengue");
        generos.add(0, "Pop");

        System.out.println(generos);

        generos.remove("Rock");

        System.out.println(generos.contains("Rock"));
        System.out.println(generos.indexOf("Vallenato"));

        for (String genero : generos) {
            System.out.println(genero.toUpperCase());
        }
    }
}

package musica.modelo;

public class Cancion {
    private String titulo;
    private String artista;
    private int duracionSegundos;

    public Cancion(String titulo, String artista, int duracionSegundos) {
        this.titulo = titulo;
        this.artista = artista;
        this.duracionSegundos = duracionSegundos;
    }

    public String getTitulo() {
        return titulo;
    }

    public void setTitulo(String titulo) {
        this.titulo = titulo;
    }

    public String getArtista() {
        return artista;
    }

    public void setArtista(String artista) {
        this.artista = artista;
    }

    public int getDuracionSegundos() {
        return duracionSegundos;
    }

    public void setDuracionSegundos(int duracionSegundos) {
        this.duracionSegundos = duracionSegundos;
    }
}


package musica.modelo;
import java.util.ArrayList;

public class Playlist {
    private String nombre;
    private ArrayList<Cancion> canciones;
    public static final int MAX_CANCIONES = 3;

    public Playlist(String nombre) {
        this.nombre = nombre;
        this.canciones = new ArrayList<>();
    }

    public boolean agregar(Cancion c) {
        if (c == null || canciones.size() >= MAX_CANCIONES || canciones.contains(c)) return false;
        canciones.add(c);
        return true;
    }

    public void mostrar() {
        System.out.println(nombre + ":");
        for (int i = 0; i < canciones.size(); i++) {
            Cancion c = canciones.get(i);
            System.out.println((i + 1) + ". " + c.getTitulo() + " " + c.getArtista() + " (" + c.getDuracion() + " s)");
        }
    }

    public int duracionTotal() {
        int suma = 0;
        for (Cancion c : canciones) suma += c.getDuracion();
        return suma;
    }

    public Cancion buscar(String titulo) {
        for (Cancion c : canciones) {
            if (c.getTitulo().equalsIgnoreCase(titulo)) return c;
        }
        return null;
    }

    public int eliminarArtista(String artista) {
        int count = 0;
        for (int i = canciones.size() - 1; i >= 0; i--) {
            if (canciones.get(i).getArtista().equalsIgnoreCase(artista)) {
                canciones.remove(i);
                count++;
            }
        }
        return count;
    }
}


package musica.app;
import java.util.ArrayList;

public class PruebaLista {
    public static void main(String[] args) {
        ArrayList<String> generos = new ArrayList<>();
        generos.add("Rock"); generos.add("Salsa"); generos.add("Vallenato");
        System.out.println(generos.size());
        System.out.println(generos.get(1));
        generos.set(1, "Merengue");
        generos.add(0, "Pop");
        System.out.println(generos);
        generos.remove("Rock");
        System.out.println(generos.contains("Rock"));
        System.out.println(generos.indexOf("Vallenato"));
        for (String g : generos) System.out.println(g.toUpperCase());
    }
}

package musica.app;
import musica.modelo.*;

public class Reproductor {
    public static void main(String[] args) {
        Cancion c1 = new Cancion("Lluvia en Manizales", "Nevado", 200);
        Cancion c2 = new Cancion("Bajo el guadual", "Café Trío", 245);
        Cancion c3 = new Cancion("Noche en Chipre", "Nevado", 185);
        Cancion c4 = new Cancion("Río Chinchiná", "Nevado", 230);

        Playlist favoritas = new Playlist("Favoritas");
        favoritas.agregar(c1); favoritas.agregar(c2); favoritas.agregar(c3);
        System.out.println(favoritas.agregar(c1)); // false
        favoritas.mostrar();
        System.out.println(favoritas.duracionTotal());

        Playlist viaje = new Playlist("Viaje");
        viaje.agregar(c1); viaje.agregar(c2);

        System.out.println(favoritas.eliminarArtista("Nevado"));
        favoritas.mostrar();
        viaje.mostrar();

        System.out.println(favoritas.buscar("bajo el guadual").getArtista());
        System.out.println(favoritas.buscar("Lluvia en Manizales"));

        System.out.println(viaje.agregar(c3));
        System.out.println(viaje.agregar(c4));
        System.out.println(Cancion.getTotalCanciones());
        System.out.println(Playlist.MAX_CANCIONES);
    }
}

package parqueadero.modelo;

public class Puesto {
    private int numero;
    private String placa;

    Puesto(int numero) {
        this.numero = numero;
        this.placa = null;
    }

    public int getNumero() { return numero; }
    public String getPlaca() { return placa; }
    public boolean estaLibre() { return placa == null; }
    public void ocupar(String placa) { this.placa = placa; }
    public void liberar() { this.placa = null; }
}

package parqueadero.modelo;
import java.util.ArrayList;

public class Parqueadero {
    private String nombre;
    private ArrayList<Puesto> puestos;
    private static int ingresosTotales = 0;

    public Parqueadero(String nombre, int cantidad) {
        this.nombre = nombre;
        this.puestos = new ArrayList<>();
        for (int i = 1; i <= cantidad; i++) puestos.add(new Puesto(i));
    }

    public static int getIngresosTotales() { return ingresosTotales; }

    public void ingresar(String placa) {
        for (Puesto p : puestos) {
            if (placa.equals(p.getPlaca())) {
                System.out.println(placa + " ya está adentro");
                return;
            }
        }
        for (Puesto p : puestos) {
            if (p.estaLibre()) {
                p.ocupar(placa);
                ingresosTotales++;
                System.out.println(placa + " en puesto " + p.getNumero());
                return;
            }
        }
        System.out.println(placa + ": parqueadero lleno");
    }

    public boolean salir(String placa) {
        for (Puesto p : puestos) {
            if (placa.equals(p.getPlaca())) {
                p.liberar();
                return true;
            }
        }
        return false;
    }

    public int puestosLibres() {
        int libres = 0;
        for (Puesto p : puestos) if (p.estaLibre()) libres++;
        return libres;
    }
}

package parqueadero.app;
import parqueadero.modelo.*;

public class Main {
    public static void main(String[] args) {
        Parqueadero centro = new Parqueadero("Centro", 2);
        Parqueadero norte = new Parqueadero("Norte", 3);

        centro.ingresar("ABC123");
        centro.ingresar("ABC123");
        centro.ingresar("XYZ789");
        centro.ingresar("JKL456");

        System.out.println(centro.salir("ABC123"));
        centro.ingresar("JKL456");
        norte.ingresar("MNO321");

        System.out.println(centro.puestosLibres());
        System.out.println(norte.puestosLibres());
        System.out.println(Parqueadero.getIngresosTotales());
    }
}

Preguntas 
1  Esto pasa porque no se pueden agregar o eliminar elementos de un `ArrayList` mientras lo recorremos con un `for-each`.
2  1. `ArrayList<int>` da error porque Java no permite usar tipos como `int` directamente. Se debe usar `Integer`.

   2. Es una relación de agregación porque una canción puede estar en varias listas al mismo tiempo. Si se elimina de una lista, sigue existiendo en la otra.

   3. `Playlist-Cancion` es agregación porque la canción puede existir fuera de la lista. `Parqueadero-Puesto` es composición porque los puestos dependen del parqueadero.

   4. `totalCanciones` es `static` porque es un contador compartido por todas las canciones. `titulo` es de instancia porque cada canción tiene su propio título.

   5. Un método `static` pertenece a la clase y no necesita crear un objeto para usarse. `this` representa al objeto actual y no se puede utilizar dentro de un método `static`.
