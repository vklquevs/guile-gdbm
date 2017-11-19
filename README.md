# Guile bindings for GDBM

## Description
This module provides functions for guile to manipulated databases
using the [gdbm](http://www.gnu.org.ua/software/gdbm/) library.

## License

guile-gdbm is licensed under the GPL version 3, as is gdbm. See
COPYING for more details.

## Example

    (use-modules (rnrs bytevector) (gdbm))

    (define db (gdbm-open "/tmp/example.db" GDBM_WRCREAT))

    (define (gdbm-set!/string db k v)
      (gdbm-set! db (string->utf8 k) (string->utf8 v)))

    (gdbm-set!/string db "foo" "bar")
    (gdbm-set!/string db "baz" "quux")
    (gdbm-set!/string db "zot" "veeblefetzer")

    (write (gdbm-fold (lambda (key value old)
                        (cons (cons (utf8->string key)
                                    (utf8->string value))
                              old))
                      '()
                      db))
    ;; (("foo" . "bar") ("zot" . "veeblefetzer") ("baz" . "quux"))

