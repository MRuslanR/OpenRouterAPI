# OpenAI Client Package

## Description

This package provides a convenient way to send requests to the OpenAI API. You can:
- Enter your API key.
- Choose a model (by default, "deepseek/deepseek-r1-zero:free" is used).
- Set system and user prompts, as well as the temperature (default is 0.7).
- Use system prompts loaded from the `system_prompts.yaml` file.

## Installation 
1. **Initialize a new Go module**:

   ```bash
   go mod init yourproject_name
   ```
2. **Add package from github**:

   ```bash
   go get github.com/MRuslanR/OpenRouterAPI
   ```
3. **Import package into your code**:
   ```go
   import "github.com/MRuslanR/OpenRouterAPI/openrouter"
   ```

4. **Install package dependencies**:

   ```bash
   go mod tidy
   ```

5. **Follow the instructions in Usage**

## Usage

```go
package main

import (
	"fmt"
	"log"
	"github.com/MRuslanR/OpenRouterAPI/openrouter" 
)

func main() {
	apiKey := ""
	model := "deepseek/deepseek-r1-zero:free"
	temperature := 0.7

	client := openrouter.NewClient(apiKey, model, temperature)

	/*
		prompts, err := openrouter.LoadSystemPrompts("system_prompts.yaml")
		if err != nil {
			log.Fatalf("Ошибка загрузки системных сообщений: %v", err)
		}
		systemPrompt, exists := prompts["default"]
		if !exists {
			log.Fatalf("Системное сообщение с ключом 'default' не найдено")
		}
	*/
	systemPrompt := ""
	userPrompt := "Who was the first person to go to space?"

	response, err := client.SendChat(systemPrompt, userPrompt)
	if err != nil {
		log.Fatalf("Ошибка отправки запроса: %v", err)
	}
	fmt.Println("Response from OpenRouter:", response)
}
```
