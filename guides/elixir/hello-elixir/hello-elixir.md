Build, Deploy, and Run an Elixir Application
============================================

Getting an application running on Fly is essentially working out how to package it as a deployable image. Once packaged it can be deployed to the Fly infrastructure to run on the global application platform. For this *Getting Started* article, we'll look at building an Elixir application from scratch.

You can follow along step-by-step in the [hello_elixir GitHub repository](https://github.com/christhekeele/fly_hello_elixir/commits/main) or clone it locally via:

```sh
git clone git@github.com:christhekeele/fly_hello_elixir.git
cd fly_hello_elixir
```

The HelloElixir Application
---------------------------

Our sample application will be a basic "hello world" example using Elixir and Plug, a lightweight webapp library. We'll be using [Elixir 1.11.3 and erlang 23.2.7](https://github.com/christhekeele/fly_hello_elixir/blob/main/.tool-versions#L1), so make sure to have these installed.

We can kick off a new Elixir application with the command `mix new hello_elixir --sup`, giving us [a starter Mix project](https://github.com/christhekeele/fly_hello_elixir/compare/mix-new~1...mix-new):

```
* creating README.md
* creating .formatter.exs
* creating .gitignore
* creating mix.exs
* creating lib
* creating lib/hello_elixir.ex
* creating lib/hello_elixir/application.ex
* creating test
* creating test/test_helper.exs
* creating test/hello_elixir_test.exs

Your Mix project was created successfully.
You can use "mix" to compile it, test it, and more:

    cd hello_elixir
    mix test

Run "mix help" for more commands.
```

We'll [add Plug and cowboy](https://github.com/christhekeele/fly_hello_elixir/compare/add-deps~1...add-deps) to our dependencies and run `mix deps.get` to install them:

```
Resolving Hex dependencies...
Dependency resolution completed:
Unchanged:
  cowboy 1.1.2
  cowlib 1.0.2
  mime 1.5.0
  plug 1.11.1
  plug_cowboy 1.0.0
  plug_crypto 1.2.1
  ranch 1.3.2
  telemetry 0.4.2
All dependencies are up to date
```

Then, we'll define [a basic Plug Router application](https://github.com/christhekeele/fly_hello_elixir/compare/add-router~1...add-router) to greet us:

```elixir
# ./lib/hello_elixir/router.ex

defmodule HelloElixir.Router do
  use Plug.Router

  plug(:match)
  plug(:dispatch)

  get "/" do
    conn
    |> send_resp(200, "<h1>Hello From Elixir on Fly!</h1>")
  end

  get "/*path" do
    conn
    |> send_resp(200, "<h1>Hello From Elixir from #{Path.join(path)} on Fly!</h1>")
  end

  match _ do
    conn
    |> send_resp(404, "<h1>No matching URL found!</h1>")
  end
end
```

After we [make the Router supervisable](https://github.com/christhekeele/fly_hello_elixir/compare/add-web~1...add-web) and [add it to our supervision tree](https://github.com/christhekeele/fly_hello_elixir/compare/start-web~1...start-web), we should be able to run it locally via `mix run --no-halt` and see it running at [localhost:4000](http://localhost:4000):

> ![Hello From Elixir on Fly!](img/hello-world.png)
>
> Hello From Elixir on Fly!

You can view the source code for this basic application [here](https://github.com/christhekeele/fly_hello_elixir/tree/basic-app) and check it out locally via `git checkout basic-app`.

Dockerizing Elixir
------------------

Fly does not (yet) provide [a pre-configured Dockerfile](https://fly.io/docs/reference/builders/#builtins) for Elixir applications, so we'll [bring our own](https://github.com/christhekeele/fly_hello_elixir/compare/add-dockerfile~1...add-dockerfile):

```Dockerfile
# ./Dockerfile

# Use exact versions selected in .tool-versions
FROM hexpm/elixir:1.11.3-erlang-23.2.7-alpine-3.13.2

# Copy the project into a working directory
RUN mkdir /app
COPY . /app
WORKDIR /app

# Install erlang package manager
RUN mix local.rebar --force
# Install Elixir package manager
RUN mix local.hex --force

# Fetch dependencies
RUN mix deps.get

# Build the project
RUN mix compile

# Run our application
CMD ["mix", "run", "--no-halt"]
```

Best practices would have us set up a [proper mix release](https://hexdocs.pm/mix/1.11.3/Mix.Tasks.Release.html) here, but this is sufficient to get us started.

To test this locally, you'll want `docker` and `docker-compose` installed. With [a little configuration](https://github.com/christhekeele/fly_hello_elixir/compare/add-docker-compose~1...add-docker-compose) we can execute `docker-compose up`, and revisit [localhost:4000](http://localhost:4000) to make sure our application is working well.

The source code for this dockerized version of our application should now look like [this](https://github.com/christhekeele/fly_hello_elixir/tree/basic-docker), see it locally via `git checkout basic-docker`.

Usual Flyctl docs can take it from here
---------------------------------------

Deep links to example incremental steps checked into repository:

- [`flyctl init`](https://github.com/christhekeele/fly_hello_elixir/compare/flyctl-init~1...flyctl-init)
- [`fly.toml`](https://github.com/christhekeele/fly_hello_elixir/compare/fly-toml~1...fly-toml)
- [`flyctl deploy`](https://github.com/christhekeele/fly_hello_elixir/compare/flyctl-deploy~1...flyctl-deploy)
- [`flyctl open`](https://github.com/christhekeele/fly_hello_elixir/compare/flyctl-open~1...flyctl-open)

Final results available in repo under tag [`basic-deploy`](https://github.com/christhekeele/fly_hello_elixir/tree/basic-deploy) or locally via `git checkout basic-deploy`.
