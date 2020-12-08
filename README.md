# Turnip CLI
An extensible C++ CLI designed for embedded systems. This example is build with
freertos/libopencm3/stm32f1, however it's straight forward to rip out the CLI part.
Please note the assets inside the `lib` folder are not covered under MIT, they have their
own licences.

## Creating commands
Each command is a seperate .h/.cpp pair (or just .h), please see `inc/hellocmd.h`
for an example. Each command should implement...

```C
virtual const char* parse(char* input)
```

The `parse` function what gets called when the user enters the command.

## Registering commands
Commands are dynamically registered like so...
```C
Cmd* menu[] = {
     new HelloCmd("hello", uart1),
     0
};
```

## Running the CLI
Just call the present function, it will not return. The first argument is the
menu shown above which is built at runtime.

```C
cli.present(menu);
```
