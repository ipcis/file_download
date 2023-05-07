Ja, das kann ich machen. Hier ist eine aktualisierte Version des Beispiels, das die URL und den Dateinamen als Argumente übergeben lässt:

```go
package main

import (
    "fmt"
    "net/http"
    "os"
    "io"
)

func main() {
    // Überprüfen, ob die korrekten Anzahl von Argumenten übergeben wurden
    if len(os.Args) < 3 {
        fmt.Println("Usage: go run main.go [URL] [file name]")
        return
    }

    // Extrahieren der URL und des Dateinamens aus den Argumenten
    fileURL := os.Args[1]
    fileName := os.Args[2]

    // Erstelle die Datei, in die wir die heruntergeladene Datei speichern werden
    file, err := os.Create(fileName)
    if err != nil {
        fmt.Println(err)
        return
    }
    defer file.Close()

    // Senden Sie eine HTTP-Anfrage an die URL der Datei
    resp, err := http.Get(fileURL)
    if err != nil {
        fmt.Println(err)
        return
    }
    defer resp.Body.Close()

    // Schreiben Sie den Inhalt der Antwort in die Datei
    _, err = io.Copy(file, resp.Body)
    if err != nil {
        fmt.Println(err)
        return
    }

    fmt.Println("File downloaded:", fileName)
}
```

Sie können das Programm wie folgt ausführen:

```
go run main.go https://example.com/file.zip file.zip
```

In diesem Beispiel wird die URL `https://example.com/file.zip` verwendet, und die heruntergeladene Datei wird im aktuellen Verzeichnis mit dem Namen `file.zip` gespeichert. Sie können jedoch den Pfad und den Dateinamen anpassen, indem Sie die Argumente ändern.
