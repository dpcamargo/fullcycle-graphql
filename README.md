# Steps
1 - printf '//go:build tools\npackage tools\nimport (_ "github.com/99designs/gqlgen"\n _ "github.com/99designs/gqlgen/graphql/introspection")' | gofmt > tools.go

2 - `go run github.com/99designs/gqlgen init`

3 - edit `schema.graphqls` and create queries, mutations and types

4 - `go run github.com/99designs/gqlgen generate`

5 - clean old code from `schema.resolvers` and implement resolvers

## Recursive categories

1 - create new individual files for recursive types and remove recursiveness from calling type

2 - add files to models in `gqlgen.yml`

3 - `go run github.com/99designs/gqlgen generate`

4 - implement new created method for resolver


# Graphiql Schema

```
mutation createCategory{
  createCategory(
  	input: {name: "Programação", description: "Cursos de Go"})
  	{id, name, description }
}

query queryCategories {
  categories {
    id
    name
    description
  }
}

query queryCategoriesWithCourses {
  categories {
    id
    name
    description
    courses {
      id
      name 
    }
  }
}

mutation createCourse {
  createCourse(
  input: {name: "Go Básico", description: "Curso de Go", categoryId: "f6b64fcf-d9ad-4536-b933-16fe9868575a"})
  {id, name, description, category: id, name, description}}

query queryCourses {
  courses {
    id
    name
    description
  }
}

query queryCoursesWithCategory {
  courses {
    id
    name
    description
    category {
      id
      name
      description
    }
  }
}
```