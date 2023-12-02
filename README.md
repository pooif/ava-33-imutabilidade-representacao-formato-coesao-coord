# 3.3 // Imutabilidade, Representação, Formato e Coesão // Coord

Use este link do GitHub Classroom para ter sua cópia alterável deste repositório: <https://classroom.github.com/a/y6Yre8De>

Implementar respeitando os fundamentos de Orientação a Objetos.

**Tópicos desta atividade:** imutabilidade, formatos de representação, formatos de entrada, coesão

---

Implementar o objeto `Coord` para a representação de coordenadas geográficas

Instâncias de `Coord` devem representar uma posição geográfica no formato de _latitude_ e _longitude_ em graus decimais, sendo que a _latitude_ vai de `-90.0` a `+90.0` e a _longitude_ de `-180.0` a `+180.0`. A construção sem argumentos de uma coordenada deve instanciar _latitude_ `0` e _longitude_ `0`. Após a construção não devem ser permitidas alterações na _latitude_ e _longitude_ a não ser que outra instância seja construída, em outras palavras, os objetos devem ser **imutáveis**.

Considere os Casos de Teste:

```java
// construtores:
Coord c1 = new Coord();
System.out.println(c1.latitude == 0.0);
System.out.println(c1.longitude == 0.0);

Coord c2 = new Coord(50.0, 134.0);
System.out.println(c2.latitude == 50.0);
System.out.println(c2.longitude == 134.0);

Coord c3 = new Coord(-90.0, -180.0);
System.out.println(c3.latitude == -90.0);
System.out.println(c3.longitude == -180.0);

// estas coordenadas são inválidas e devem lançar exceção
// faça serem rejeitadas e depois comente-as para não parar o programa
new Coord(-91.0, 0.0);
new Coord(100.0, 0.0);
new Coord(10.0, -182.0);
new Coord(10.0, 200.0);
new Coord(-95.0, -200.0);

// imutabilidade: as linhas a seguir devem causar erro de compilação
// verifique se está de acordo e depois comente-as
Coord c4 = new Coord();
c4.latitude = 30.0;  // não deve permitir reatribuição
c4.longitude = 80.0; // não deve permitir reatribuição

// operações/comandos:
Coord in = new Coord(30.0, 50.0);
Coord out = in.norte(5.0);
System.out.println(in.latitude == 30.0); // deve ser imutável
System.out.println(out.latitude == 35.0);
out.norte(5.0); // sem reatribuição sem alteração
System.out.println(out.latitude == 35.0);
out = out.norte(5.0); // reatribuindo
System.out.println(out.latitude == 40.0);
out = out.sul(60.0);
System.out.println(out.latitude == -20.0);
out = out.sul(30.0);
System.out.println(out.latitude == -50.0);
out = out.sul(-10.0);
System.out.println(out.latitude == -40.0);
out = out.norte(-10.0);
System.out.println(out.latitude == -50.0);
System.out.println(out.longitude == 50.0);
out = out.leste(50.0);
System.out.println(out.longitude == 100.0);
out = out.oeste(180.0);
System.out.println(out.longitude == -80.0);
out = out.oeste(-10.0);
System.out.println(out.longitude == -70.0);
out = out.leste(-10.0);
System.out.println(out.longitude == -80.0);

// consultas:
Coord q = new Coord();
System.out.println(q.latitude == 0);
System.out.println(q.longitude == 0);
System.out.println(q.noEquador() == true);
System.out.println(q.emGreenwich() == true);
q = q.norte(10.0);
System.out.println(q.latitude == 10);
System.out.println(q.noEquador() == false);
q = q.leste(10.0);
System.out.println(q.emGreenwich() == false);
q = q.leste(170.0);
System.out.println(q.longitude == 180.0);
System.out.println(q.emGreenwich() == false);
q = q.oeste(200.0);
System.out.println(q.longitude == -20.0);
System.out.println(q.emGreenwich() == false);
q = q.leste(5.0).leste(5.0).leste(5.0).leste(5.0);
System.out.println(q.longitude == 0.0);
System.out.println(q.emGreenwich() == true);

Coord r = new Coord(30.0, 70.0);
System.out.println(r.latitude == 30.0);
System.out.println(r.longitude == 70.0);
System.out.println(r.noNorte() == true);
System.out.println(r.noSul() == false);
System.out.println(r.noOriente() == true);
System.out.println(r.noOcidente() == false);
r = r.oeste(140.0).sul(60.0);
System.out.println(r.latitude == -30.0);
System.out.println(r.longitude == -70.0);
System.out.println(r.noNorte() == false);
System.out.println(r.noSul() == true);
System.out.println(r.noOriente() == false);
System.out.println(r.noOcidente() == true);
```

**Informações adicionais:**

- Imagem esclarecedora <http://eogn.com/images/newsletter/2014/Latitude-and-longitude.png>
- Sobre coordenadas decimais <http://opussig.blogspot.com.br/2013/01/coordenadas-geograficas-em-formato.html>

Implementar os métodos de conversão para `Coord` conforme os casos de teste.

```java
// As coordenadas entram em graus decimais com até quatro casas decimais
Coord coord1 = new Coord(12.5334, 77.2635);
System.out.println(coord1.toString()); // 12.5334, 77.2635
System.out.println(coord1.toString().equals("12.5334, 77.2635"));
// Não confunda o símbolo de grau ° com o de número ordinal º
System.out.println(coord1.toGrausDecimais()); // 12.5334°N, 77.2635°E
System.out.println(coord1.toGrausDecimais().equals("12.5334°N, 77.2635°E"));
// Em Graus, Minutos e Segundos com 3 decimais
System.out.println(coord1.toGrausMinutosSegundos()); // 12°32'0.240"N, 77°15'48.600"E
System.out.println(coord1.toGrausMinutosSegundos().equals("12°32'0.240\"N, 77°15'48.600\"E"));

Coord coord2 = new Coord(-75.9923, -52.1425);
System.out.println(coord2.toString()); // -75.9923, -52.1425
System.out.println(coord2.toString().equals("-75.9923, -52.1425"));
System.out.println(coord2.toGrausDecimais(); // 75.9923°S, 52.1425°W
System.out.println(coord2.toGrausDecimais().equals("75.9923°S, 52.1425°W"));
System.out.println(coord2.toGrausMinutosSegundos()); // 75°59'32.280"S, 52°8'33.000"W
System.out.println(coord2.toGrausMinutosSegundos().equals("75°59'32.280\"S, 52°8'33.000\"W"));

Coord coord3 = Coord.fromString("63°18'12.300\"S, 76°56'43.120\"W");
System.out.println(coord3.toString()); // -63.3034, -76.9453
System.out.println(coord3.toString().equals("-63.3034, -76.9453")); // -63.3034, -76.9453

Coord coord4 = Coord.fromString("-63.3034, -76.9453");
System.out.println(coord4.toGrausMinutosSegundos().equals("63°18'12.240\"S, 76°56'43.080\"W"));
```

**Conversor de Coordenadas:** <http://maps.marnoto.com/conversor-coordenadas/>.

---
Obs.: os casos de teste não podem ser alterados, mas outros podem ser adicionados. Fique a vontade para adicionar códigos que imprimem ou separam os testes, por exemplo.
