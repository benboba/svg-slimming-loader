# svg-slimming-loader

[webpack](https://github.com/webpack/webpack) loader plugin, read svg file and use [svg-slimming](https://github.com/benboba/svg-slimming) for compression

## Basic usage

Basic usage depends on file-loader. The reference configuration of webpack.config.js is as follows:
```js
module.exports = {
    ...
    module: {
        rules: [
            ...
            {
                test: /\.svg$/,
                use: [
                    'file-loader',
                    'svg-slimming-loader'
                ]
            }
            ...
        ]
    },
    ...
}
```

## Export to js module

This usage does not need to rely on file-loader, you need to set isModule to true in options. The reference configuration of webpack.config.js is as follows:
```js
module.exports = {
    ...
    module: {
        rules: [
            ...
            {
                test: /\.svg$/,
                use: [
                    {
                        loader: 'svg-slimming-loader',
                        options: {
                            isModule: true
                        }
                    }
                ]
            }
            ...
        ]
    },
    ...
}
```

This usage will export the svg file as a js module

## Use custom optimization rules

Just configure rules in options. For detailed configuration, please refer to [documentation of svg-slimming](https://github.com/benboba/svg-slimming/blob/master/README.md). The reference configuration of webpack.config.js is as follows:
```js
module.exports = {
    ...
    module: {
        rules: [
            ...
            {
                test: /\.svg$/,
                use: [
                    {
                        loader: 'svg-slimming-loader',
                        options: {
                            rules: {
                                'shorten-decimal-digits': [true, {
                                    "angelDigit": 1,
                                    "sizeDigit": 0
                                }],
                                'shorten-style-attr': [true, {
			                        "exchange": true
                                }]
                            }
                        }
                    }
                ]
            }
            ...
        ]
    },
    ...
}
```

## Use Optimization Rule Configuration File

Configure configPath in options, the target can be a file in json format. It also supports the isModule and rules attributes:
```js
module.exports = {
    ...
    module: {
        rules: [
            ...
            {
                test: /\.svg$/,
                use: [
                    {
                        loader: 'svg-slimming-loader',
                        options: {
                            configPath: './svg-slimming.config.json'
                        }
                    }
                ]
            }
            ...
        ]
    },
    ...
}
```

The svg-slimming.config.json reference is as follows:
```js
{
    "isModule": true,
    "rules": {
        "shorten-decimal-digits": [true, 0, 0],
        "shorten-style-attr": [true, true]
    }
}
```

**Note that when options and config files have both isModule and rules configurations, the options configuration takes precedence**
