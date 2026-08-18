# Grammar

This is the complete Kina language grammar defined using the Extended BNF notation.

## Lexical grammar

Every character is significant here.

    SourceChar            := any UTF-8 character

    LineTerminator        := "\n" | "\r\n" | "\r"
    Whitespace            := " " | "\t" | LineTerminator

    Comment               := LineComment | BlockComment
    LineComment           := "//" (SourceChar - LineTerminator)*
    BlockComment          := "/*" SourceChar* "*/"
