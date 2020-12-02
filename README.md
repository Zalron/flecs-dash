# flecs-dash
Web-based dashboard for flecs. This project is still under development and may change a lot!

## Usage
The dashboard requires the following modules:

Module      | Description      
------------|------------------
[flecs.meta](https://github.com/flecs-hub/flecs-meta) | Reflection for Flecs components
[flecs.json](https://github.com/flecs-hub/flecs-json) | JSON serializer for Flecs components
[flecs.rest](https://github.com/flecs-hub/flecs-rest) | A REST interface for introspecting & editing entities
[flecs.monitor](https://github.com/flecs-hub/flecs-monitor) | Web-based monitoring
[flecs.player](https://github.com/flecs-hub/flecs-player) | Play, stop and pause simulations
[flecs.components.http](https://github.com/flecs-hub/flecs-components-http) | Components describing an HTTP server
[flecs.systems.civetweb](https://github.com/flecs-hub/flecs-systems-civetweb) | HTTP server implementation
[flecs.dash](https://github.com/flecs-hub/flecs-dash) | The dashboard (this project)

1. Add the module source & header file (from the repository root) to your project for each dependency
2. Copy the `etc` directory from the `flecs.dash` repository to your project root. 
3. Configure a threading implementation in the OS API (see below)

To add the dashboard to a C application, do:
```c
ECS_IMPORT(world, FlecsDash);
ECS_IMPORT(world, FlecsSystemsCivetweb);

ecs_set(world, 0, EcsDashServer, {.port = 9090});
```
To add it to a C++ application, do:
```cpp
world.import<flecs::dash>();
world.import<flecs::systems::civetweb>();

ecs.entity().set<flecs::dash::Server>({9090});
```

Make sure to start your application from the project root. This ensures that the dashboard code can find the web resources. Go to `http://localhost:9090` to open the dashboard.

## Setting up OS API
The webserver requires a threading implementation to be configured in the Flecs OS API. You can do this yourself, or add this example as a dependency to your project:
https://github.com/SanderMertens/flecs/tree/master/examples/os_api/flecs-os_api-posix. When using this example, make sure to add this before creating the world:

```c
posix_set_os_api();
```

## Screenshot

<img width="1117" alt="Screen Shot 2020-11-26 at 8 14 43 PM" src="https://user-images.githubusercontent.com/9919222/100412011-39b63680-3028-11eb-87ca-406f905ca037.png">
