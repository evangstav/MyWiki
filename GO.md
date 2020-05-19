# GO

## Echo1
``` go
var s, sep string %variable declaration
    for i := 1; i < len(os.Args); i++ {
        s += sep + os.Args![pic](i)
        sep = " "
    }
    fmt.Println(s)
  ```
  
  
  
## Echo2
``` go
s, sep := "", ""  %variable declaration
    for _, arg := range os.Args![pic](1:) {
        s += sep + os.Args![pic](i)
        sep = " "
    }
    fmt.Println(s)
  ```
