@def title = "Blog"

```julia:./list-posts.jl
#hideall
using Dates
dir = "_posts"
for year in reverse(readdir(dir))
  println("## $year")
  for fmd in reverse(readdir(joinpath(dir, year)))
    f = split(fmd, ".")[1]
    path = joinpath(dir, year, f)
    println("- {{fill date $path}}, [{{fill title $path}}]($path)")
  end
end
```

\textoutput{./list-posts}
