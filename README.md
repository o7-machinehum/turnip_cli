# Turnip CLI
An extensible C++ CLI designed for embedded systems.

## Creating commands
Each command is a seperate .h/.cpp pair (or just .h), please see src/hellocmd.h
for an example. Each command should implement...

```C
virtual const char* parse(char* input)
```

This is the function that gets called when the user enters the command

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
menu shown above.

```C
cli.present(menu);
```
