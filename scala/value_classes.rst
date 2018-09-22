Value classes
=============

https://docs.scala-lang.org/overviews/core/value-classes.html

ivan.kliuk@Typhoon:~$ javap Identifier.class
Compiled from "ValueClass.scala"
public class Identifier {
  public int id();
  public Identifier(int);
}
ivan.kliuk@Typhoon:~$ less ValueClass.scala
ivan.kliuk@Typhoon:~$ javap IdentifierVal.class
Compiled from "ValueClass.scala"
public final class IdentifierVal {
  public static boolean equals$extension(int, java.lang.Object);
  public static int hashCode$extension(int);
  public int id();
  public int hashCode();
  public boolean equals(java.lang.Object);
  public IdentifierVal(int);
}
ivan.kliuk@Typhoon:~$ rm IdentifierVal.class
ivan.kliuk@Typhoon:~$ rm IdentifierVal\$.class
ivan.kliuk@Typhoon:~$ rm Identifier
Identifier$.class  Identifier.class
ivan.kliuk@Typhoon:~$ rm Identifier*
ivan.kliuk@Typhoon:~$ javap IdentifierVal.class
Error: class not found: IdentifierVal.class
ivan.kliuk@Typhoon:~$ scalac ValueClass.scala
ivan.kliuk@Typhoon:~$ javap Identifier.class
Compiled from "ValueClass.scala"
public class Identifier {
  public int id();
  public Identifier(int);
}
ivan.kliuk@Typhoon:~$ javap IdentifierVal.class
Compiled from "ValueClass.scala"
public final class IdentifierVal {
  public static boolean equals$extension(int, java.lang.Object);
  public static int hashCode$extension(int);
  public int id();
  public int hashCode();
  public boolean equals(java.lang.Object);
  public IdentifierVal(int);
}
ivan.kliuk@Typhoon:~$ vim ./Identifier.class
ivan.kliuk@Typhoon:~$ vim ValueClass.scala
ivan.kliuk@Typhoon:~$ git diff
ivan.kliuk@Typhoon:~$ javap IdentifierVal.class
