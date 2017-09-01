---
layout: post
title: "Lightweigth microservices with Go"
author: pablo
date: 2017-07-25 19:00:00
description: ¡Realiza tus microservicios con Go!
tags: Microservices Golang 
categories: Microservices
twitter_text: Lightweigth microservices with Go
---


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

Para arrancar nuestro microservicio solo tenéis que ejecutar la siguiente linea de comandos.

```shell

go run notes_microservice.go

```


