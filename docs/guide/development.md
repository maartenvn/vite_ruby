[tag helpers]: /guide/rails.html#tag-helpers-%F0%9F%8F%B7
[discussions]: https://github.com/ElMassimo/vite_ruby/discussions
[rails]: https://rubyonrails.org/
[webpacker]: https://github.com/rails/webpacker
[vite rails]: https://github.com/ElMassimo/vite_ruby
[vite]: https://vitejs.dev/
[vite-templates]: https://github.com/vitejs/vite/tree/main/packages/create-app
[plugins]: https://vitejs.dev/plugins/
[configuration reference]: /config/
[build]: /config/#build-options
[dev options]: /config/#development-options
[json config]: /config/#shared-configuration-file-%F0%9F%93%84
[vite config]: /config/#configuring-vite-%E2%9A%A1
[sourceCodeDir]: /config/#sourcecodedir
[autoBuild]: /config/#autobuild
[entrypoints]: https://vitejs.dev/guide/build.html#multi-page-app
[vite_client_tag]: https://github.com/ElMassimo/vite_ruby/blob/main/lib/vite_rails/helper.rb#L13-L17
[vite_javascript_tag]: https://github.com/ElMassimo/vite_ruby/blob/main/lib/vite_rails/helper.rb#L28-L51
[vite_typescript_tag]: https://github.com/ElMassimo/vite_ruby/blob/main/lib/vite_rails/helper.rb#L57-L59
[vite_stylesheet_tag]: https://github.com/ElMassimo/vite_ruby/blob/main/lib/vite_rails/helper.rb#L62-L64
[vite_asset_path]: https://github.com/ElMassimo/vite_ruby/blob/main/lib/vite_rails/helper.rb#L23-L25

# Developing with Vite

In this section, we'll cover the basics to get started with Vite in Ruby web apps.

## Development Server 💻

Run <kbd>bin/vite dev</kbd> to start a Vite development server.

It will read your [`config/vite.json`][json config] configuration, which can be
used to configure the `host` and `port`, as well as [other options][dev options].

## Auto-Build 🤖

Even when not running the Vite development server, _Vite Ruby_ can detect if
any assets have changed in [`sourceCodeDir`][sourceCodeDir], and trigger a build
automatically when the asset is requested.

This is very convenient when running integration tests, or when a developer
does not want to start the Vite development server (at the expense of a slower feedback loop).

::: tip Enabled locally
By [default][json config], [`autoBuild`][autoBuild] is enabled in the <kbd>test</kbd> and <kbd>development</kbd> environments.
:::

## Entrypoints ⤵️

Drawing inspiration from [webpacker], any files in [`app/frontend/entrypoints`][build]
will be considered [entries][entrypoints] to your application (SPAs or pages).

```
app/frontend:
  ├── entrypoints:
  │   # only Vite entry files here
  │   └── application.js
  │   └── typography.css
  └── components:
  │   └── App.vue
  └── channels:
  │   │── index.js
  │   └── chat.js
  └── stylesheets:
  │   └── my_styles.css
  └── images:
      └── logo.svg
```

These files will be automatically detected and passed on to Vite, all [configuration][entrypoints] is done
for you.

You can add them to your HTML layouts or views using the provided [tag helpers].

## Import Aliases 👉

For convenience, a `~/` import alias is configured to `app/frontend`, allowing
you to use absolute paths:

```js
import App from '~/components/App.vue'
import '~/channels'
```

## CLI Commands ⌨️

A CLI tool is provided, you can run it using `bundle exec vite`, or `bin/vite` after installation.

- <kbd>bundle exec vite install</kbd>:
  Install configuration files and sample setup for your web app

- <kbd>bin/vite dev</kbd>:
  Starts the Vite development server

- <kbd>bin/vite build</kbd>:
  Makes a production bundle with Vite using Rollup behind the scenes

- <kbd>bin/vite info</kbd>:
  Provide information on _Vite Ruby_ and related libraries

::: tip Environment-aware

All these commands are aware of the environment. When running them locally in
development you can provide `RACK_ENV=production` to simulate a production build.
:::
