# Module

A Module is an abstraction of a feature in our city (e.g., Intersection Controller, Smart Bike Parking, etc.). Each Module supports CRUD operations to make our microcontrollers customizable and generic. These modules support commands, which typically come from the API running on the microcontroller but can also be created and used easily in tests.

## Class Overview

The `Module` class is defined in `embedded/lib/Module/Module.h` and serves as the base class for all city features. It inherits from `IJsonSerializable` to enable JSON-based serialization and deserialization.

## Management

Modules are managed by the `ModuleContext` class (`embedded/lib/ModuleContext/ModuleContext.h`), which provides CRUD operations:

- **createModule**: Creates a new module instance using the factory pattern.
- **getModule**: Retrieves a module by ID.
- **updateModule**: Updates a module's state from JSON.
- **deleteModule**: Removes a module instance.

The context holds up to 15 modules in an array of pointers.

## Factory Pattern

Module creation uses the factory pattern via `IModuleFactory` (`embedded/lib/IModuleFactory/IModuleFactory.h`). The concrete implementation `ConcreteModuleFactory` is responsible for instantiating specific module types based on the `moduleType` string.

Currently, the factory returns `nullptr` as a placeholder; subclasses of `Module` (e.g., specific controllers) should be implemented and registered here.

## Example Usage

In `embedded/src/main.cpp`, the system initializes a `ModuleContext` with a `ConcreteModuleFactory`. Modules are created, updated, and managed through this context, allowing dynamic configuration of city features.

## Enabling Features
Because ESPs have limited memory, we want to limit the size of the sketch uploaded. This is done by optionally including 
modules in our ConcreteModuleFactory class. In order to enable a feature when compiling the code, we simply include a 
compiler flag. An example of this is -DINTERSECTION_CONTROLLER. We use a flag for each feature we want enabled, or 
add in the -DENABLE_ALL_MODULES flag to enable everything.

## Additonaly Docs
Documentation for the `Module` class exists in the header file as Doxygen-style comments.

See `embedded/lib/Module/Module.h` for detailed class and method documentation.