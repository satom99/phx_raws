# phx_raws

*phx_raws* provides a raw websocket server on top of [Phoenix](https://github.com/phoenixframework/phoenix)' implementation.

##### Example
```elixir
defmodule Example.Gateway do
  use Phoenix.Socket

  transport :gateway, Phoenix.Transports.WebSocket.Raw

  def connect(_params, socket) do
    send self(), {:text, "Welcome!"}

    {:ok, socket}
  end

  def id(socket), do: nil

  def handle(:text, message, _state) do
    IO.inspect message
    #| :ok
    #| state
    #| {:text, message}
    #| {:text, message, state}
    #| {:close, "Goodbye!"}
    {:text, message}
  end

  def handle(:closed, reason, _state) do
    IO.inspect reason
  end
end
```
