Function composition
====================

Generally, function composition can be applied only on function with one
parameter. To perform functional composition on function with more
than one parameter represent it as a set of functions with one parameter.

**Functions in Scala**

A function with no argument has only one method:

.. code-block:: scala
    :caption: Function0 rough definition

        trait Function0[+R] extends AnyRef { self =>
          def apply(): R
        }

`compose` and `andThen` exist only for function with one argument.

.. code-block:: scala
    :caption: Function1 rough definition

    trait Function1[-T1, +R] extends AnyRef { self =>
      def apply(v1: T1): R
      def compose[A](g: A => T1): A => R = { x => apply(g(x)) }
      def andThen[A](g: R => A): T1 => A = { x => g(apply(x)) }
    }

.. code-block:: scala
    :caption: Function composition

    val getStringLength = (s: String) => s.length
    // getStringLength: String => Int = $$Lambda$5501/1320792033@42cb004b

    val double = (a: Int) => a * 2
    // double: Int => Int = $$Lambda$5523/1381464362@42ee8e68

    getStringLength andThen double
    // res0: String => Int = scala.Function1$$Lambda$5531/570615914@73d10146

    res0("Hello world!")
    // res1: Int = 24

    double compose getStringLength
    // res2: String => Int = scala.Function1$$Lambda$5577/1419413857@1edaffff

    res2("Hello world!")
    // res3: Int = 24

`tupled` creates a tupled version of the function: instead of `n` arguments,
it accepts a single tuple argument. It can be helpful if you need to compose
functions with more that one argument:

.. code-block:: scala
    :caption: Function2 rough definition

        trait Function2[-T1, -T2, +R] extends AnyRef { self =>
          def apply(v1: T1, v2: T2): R
          def curried: T1 => T2 => R = { (x1: T1) => (x2: T2) => apply(x1, x2) }
          def tupled: Tuple2[T1, T2] => R = { case Tuple2(x1, x2) => apply(x1, x2) }
        }

.. code-block:: scala
    :caption: Composition of functions with more than one argument

    val sum = (x: Int, y: Int) => x + y
    // sum: (Int, Int) => Int = $$Lambda$6297/2018725025@4e988072

    val multiplyBy2 = (a: Int) => a * 2
    // multiplyBy2: Int => Int = $$Lambda$6380/1906993348@1f5b9821

    sum.tupled andThen multiplyBy2
    // res1: ((Int, Int)) => Int = scala.Function1$$Lambda$6382/1216992973@bb8e009

    res1((1,2))
    // res2: Int = 6

    // Newly created function accepts a tuple of arguments. It can be easily untupled:

    Function.untupled(res1)
    // res3: (Int, Int) => Int = scala.Function$$$Lambda$6404/1694053404@274a4d89

    res3(1,2)
    // res4: Int = 6
