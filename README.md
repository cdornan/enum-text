# enum-text

A simple toolkit for rendering enumerated types into `Text` `Builder` (used by
the [`fmt`](http://hackage.haskell.org/package/fmt) package) and parsing them
back again into Text with the provided `TextParsable` type class.

To get the `Buildable` and `TextParsable` instances for an enumerated data type
use the following pattern:

```
import Fmt
import Text.Enum.Text

data Foo = FOO_bar | FOO_bar_baz
  deriving (Bounded,Enum,Eq,Ord,Show)

instance EnumText     Foo
instance Buildable    Foo where build     = buildEnumText
instance TextParsable Foo where parseText = parseEnumText
```

This will use the default configuration for generating the text of each
enumeration from the derived `show` text, namely:

  * removing the prefix upto and including the first underscore (`_`);
  * converting each subsequent underscore (`_`) into a dash (`-`).

See the Haddocks for details on how to override this default configuration for
any given enumeration type.

Functions for rendering text, generating and parsing UTF-8 encoded ByteStrings
(suitable for cassava) and `Hashable` functions are also provided `EnumText`.