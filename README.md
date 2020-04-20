# awesome-obfuscator-loader

Fork of [obfuscator-loader](https://github.com/javascript-obfuscator/obfuscator-loader) with Node 12 support.

This is a module loader for webpack wich obfuscate module source code using [javascript-obfuscator](https://github.com/javascript-obfuscator/javascript-obfuscator).  

## Installation
```npm install --save-dev awesome-obfuscator-loader```


## Why not a plugin?
Obfuscating code can results in quite large files. It's a good idea to obfuscate only your code leaving third party libraries unobfuscated.
This is simple to achieve using a plugin if you plan to split your code and third party code in different bundles. Take a look at [this plugin](https://github.com/javascript-obfuscator/webpack-obfuscator).  


Sometimes you need to output a single js bundle but you still need to obfuscate the source code of some particular module. In these cases a loader can do the trick.  
For example I happened to had to bundle a big third party library (not a module of any sort, I had to use [script-loader](https://github.com/webpack-contrib/script-loader)) in one of my project and I was requested to obfuscate my code. 

## Usage
Define a rule in your webpack config and use the obfuscator-loader as the last of your loaders for your modules. You can add the **enforce: 'post'** flag to ensure the loader will be called after normal loaders:

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        include: [ path.resolve(__dirname, "justMySources") ],
        enforce: 'post',
        use: { loader: 'obfuscator-loader', options: {/* options here */} }
      },
    ]
  }
};
```

## Options
This loader accepts the same options object of [javascript-obfuscator](https://www.npmjs.com/package/javascript-obfuscator#options)
