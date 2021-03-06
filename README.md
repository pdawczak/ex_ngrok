# ex_ngrok

A wrapper around [Ngrok](https://ngrok.com/) providing a secure tunnel to localhost for demoing your Elixir/Phoenix web application or testing webhook integrations.

Once installed, ex_ngrok will manage starting and stopping Ngrok with your application and expose Ngrok's settings to your application.

## Dependencies

- **[Ngrok](https://ngrok.com/) 2.x** Install it on OSX with:

        $ brew cask install ngrok

## Installation

Add ex_ngrok to your `mix.exs` dependencies:

```elixir
def deps do
  [{:ex_ngrok, github: "joshuafleck/ex_ngrok", only: [:dev]}]
end

def application do
  [ applications: [:ex_ngrok] ]
  # Application dependency auto-starts it, otherwise: Application.start(:ex_ngrok)
end
```

## Configuration

You will need to set the following configuration variables in your `config/config.exs` file:

```elixir
config :ex_ngrok,
  # The name of the Ngrok executable
  executable: "ngrok",
  # The type of tunnel
  protocol: "http",
  # The port to which Ngrok will forward requests
  port: "4000",
  # The URL of Ngrok's API (used to retrieve its settings)
  api_url: "http://localhost:4040/api/tunnels"
```

## Usage

### Retrieving your public URL

Ngrok will create a public URL that tunnels to your development machine.
The URL will change every time Ngrok starts, but you can retrieve the URL
by running the following:

```elixir
Ngrok.Settings.get("public_url") # => http://(.*).ngrok.io/
```
