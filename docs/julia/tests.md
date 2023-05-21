# Tests

Add `Tests` package

```sh
(MyProject) pkg> add Test
```

Create `test/runtests.jl` file with the following content

```julia
using SomeProject
using Test

@testset "Example tests" begin
    @testset "Math tests" begin
        @test true
    end
end
```

Run tests

```sh
(MyProject) pkg> test
```
