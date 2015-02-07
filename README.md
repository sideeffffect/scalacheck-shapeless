# scalacheck-shapeless

Generation of arbitrary case classes / ADTs with [scalacheck](https://github.com/rickynils/scalacheck) and [shapeless](https://github.com/milessabin/shapeless)

## Usage

Add to your `build.sbt`
```scala
libraryDependencies +=
  "com.github.alexarchambault" %% "scalacheck-shapeless" % "1.12.1"
```

If you are using scala 2.10.x, also add the macro paradise plugin to your build,
```scala
libraryDependencies +=
  compilerPlugin("org.scalamacros" % "paradise" % "2.0.1" cross CrossVersion.full)
```


Import the content of `org.scalacheck.Shapeless` close to where you want
`Arbitrary` type classes to be automatically available for case classes
/ sealed hierarchies,
```scala
import org.scalacheck.Shapeless._

//  If you defined:

// case class Foo(i: Int, s: String, blah: Boolean)
// case class Bar(foo: Foo, other: String)

// sealed trait Base
// case class BaseIntString(i: Int, s: String) extends Base
// case class BaseDoubleBoolean(d: Double, b: Boolean) extends Base

//  then you can now do

implicitly[Arbitrary[Foo]]
implicitly[Arbitrary[Bar]]
implicitly[Arbitrary[Base]]
```

and in particular, while writing property-based tests,
```scala
property("some property about Foo") {
  forAll { foo: Foo =>
    // Ensure foo has the required property
  }
}
```
without having to define yourself an `Arbitrary` for `Foo`.

For the development version (new versioning), add instead to your `build.sbt`
```scala
resolvers += Resolver.sonatypeRepo("snapshots")

libraryDependencies +=
  "com.github.alexarchambault" %% "scalacheck-shapeless_1.12" % "0.1.0-SNAPSHOT"
```

(Macro paradise plugin also necessary with scala 2.10, see above.)

Available for scala 2.10 and 2.11. Uses scalacheck 1.12.1 and shapeless 2.1.0-RC1.

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/alexarchambault/scalacheck-shapeless?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
