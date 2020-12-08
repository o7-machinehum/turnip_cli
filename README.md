# Turnip CLI
An extensible C++ CLI (Command line interface) designed for embedded systems.
This example is built with freertos/libopencm3/stm32f1, however it's straight
forward to rip out the CLI part. Please note the assets inside the `lib`
folder are not covered under MIT, they have their own licences.

## Creating commands
Each command is a seperate `.h/.cpp` pair (or just `.h`), please see `inc/hellocmd.h`
for an example. Each command class should implement...

```C
virtual const char* parse(char* input)
```


The `parse` function what gets called when the user enters the command. The class should also
inherit from from the Cmd class. Just look at the code you should be able to figure it out.

## Registering commands
Commands are dynamically registered like so...
```C
Cmd* menu[] = {
     new HelloCmd("hello", uart1),
     0
};
```

## Running the CLI
Just call `present()`, it will not return. The first argument is the menu shown
above which is built at runtime.

```C
cli.present(menu);
```

## Building
```bash
git clone https://github.com/Machine-Hum/turnip_cli
cd turnip_cli
git submodule update --init --recursive
cd lib/libopencm3
make
cd ../..
make
make flash 
```
