Doing things remotely, push to dockerhub then run on cluster worked better than having cluster environments to build.

Base images: alpine very small, python included. Maybe have options, but should try using this.

Consider installing dev tools, compiling what's needed, then removing tools to keep size small.

Developing containers, go big first then split into components as it makes sense.

Do consider not reimplementing the wheel, good options out there but may need patches.

Microservices, separate for different languages, etc.

"Official" version, 

We went to genomics, for compose.