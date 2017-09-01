---
layout: post
title: "Lightweigth microservices with Go"
author: pablo
date: 2017-09-04 00:00:00
description: ¡Realiza tus microservicios con Go!
tags: Microservices Golang 
categories: Microservices
twitter_text: Lightweigth microservices with Go
---

Hoy me gustaría poner ante vosotros una manera de realizar microservicios de una manera sencilla y ligera y ya que estamos que nos llegará a los más nostálgicos al corazón :). Aunque seguro que la mayoría de vosotros conocéis [Go](https://golang.org/), el lenguaje de Google que nació en 2007, Go es un lenguaje cuya sintaxis está derivada de **C** y que añade algunas funcionalidades muy conocidas por los Javeros como pueden ser el recolector de basura, además de permitirnos crear scripts muy consistentes y eficientes.

Para ello hoy os prongo un script de Go que nos permite lanzar un microservicio para tener una lista de notas y tareas para que no olvidemos aquello más importante de nuestro día a día. Por simplificar este servicio solo permitiremos crear nuevas notas y listar aquellas que ya hemos creado.

#### notes_microservice.go

```golang
package main

import (
    "encoding/json"
    "net/http"
    "time"
)

type Note struct {
	Id	int
	Content string
	Date time.Time
}

type Message struct {
	message string
}

var Notes []Note

func handler(response http.ResponseWriter, request *http.Request) {
    switch request.Method {
		case "GET":
			listNotes(response,request)
		case "POST":
			createNote(response,request)
		default:
			returnMessage(response,request,"Method not allowed")
	}
}
 
func main() {
    http.HandleFunc("/notes", handler)
    http.ListenAndServe(":8080", nil)
}
 
func createNote (response http.ResponseWriter, request *http.Request) {
	note := Note{}
	
	error := json.NewDecoder(request.Body).Decode(&note)
		
	if error != nil {
		panic(error)
	}
	note.Id = len(Notes);
	note.Date = time.Now().Local()
	Notes = append(Notes,note)
	responseObject, error := json.Marshal(note)
	
	if error != nil {
		panic(error)
	}
	
    response.Write(responseObject)
}

func listNotes (response http.ResponseWriter, request *http.Request) {
	
	responseObject, error := json.Marshal(Notes)
	
	if error != nil {
		panic(error)
	}
	
    response.Write(responseObject)
}

func returnMessage (response http.ResponseWriter, request *http.Request, message string) {
 
    m := Message{message}
    bodyMessage, error := json.Marshal(m)

    if error != nil {
        panic(error)
    }
	
    response.Write(bodyMessage)
}
```

Cabe destacar que nuestro microservicio guarda en memoria las notas que vayamos creando. Como buenos *Geeks* os animo a que utilicéis estás pequeñas directrices para hacer vuestros microservicios utilizando persistencia.

Para arrancar vuestro microservicio solo tenéis que ejecutar la siguiente linea de comandos.

```shell

go run notes_microservice.go

```

Ahora solo tenéis que hacer vuestras peticiones GET (para el listado de notas) y POST (para crear nuevas notas) a *localhost:8080/notes*. Os dejo algún json de ejemplo para ir creando vuestras primeras notas.

```json
	{
        "content" : "Comprar el pan"
    }
```

Espero que os haya sido de ayuda.


