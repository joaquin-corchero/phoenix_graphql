[![Build Status](https://travis-ci.org/joaquin-corchero/phoenix_graphql.svg?branch=master)](https://travis-ci.org/joaquin-corchero/phoenix_graphql)
# Phoenix and Graphql

Little application showcasing phoenix with graphql using absinthe_plug with json as datasource.

I hope the names on the modules will make easier to understand how things fit together.

To start your Phoenix app:

* Install dependencies with `mix deps.get`
* Start Phoenix endpoint with `mix phoenix.server`

##Once the site is running:

###Go here to play with queries[`localhost:4000/graphiql`](http://localhost:4000/graphiql) to run queries like:  
```
{
  root{
    posts{
      body,
      id,
      title
    }
    users{
      email,
      name,
      id
    }
    filteredUser(id:"1"){  
      id,  
      name,  
      email  
  	}  
  }
}
```

###Mutation relay example:
```
payload field :post_model do
  input do
    field :title, non_null(:string)
    field :body, non_null(:string)
  end
  output do
    field :title, :string
    field :body, :string
  end
  resolve &PostDto.create/2
end
```

###Execution on graphiql:
```
mutation M($input: PostModelInput){  
  postModel(input: $input){  
    clientMutationId,  
    body,  
    title  
  }  
}
```

query variables:  
```
{  
  "input": {  
    "title": "Post title",  
    "body":  "Post body",  
    "clientMutationId": "post001"  
  }  
}
```

###Run queries directly like:  [`localhost:4000/api?query={root{posts{body,id,title}}}`](http://localhost:4000/api?query={root{posts{body,id,title}}})  

## Learn more

* Official website: http://www.phoenixframework.org/
* Guides: http://phoenixframework.org/docs/overview
* Docs: https://hexdocs.pm/phoenix
* Mailing list: http://groups.google.com/group/phoenix-talk
* Source: https://github.com/phoenixframework/phoenix
* absinthe_plug: https://github.com/absinthe-graphql/absinthe_plug
* graphql: http://graphql.org/learn/
* stubr: https://github.com/leighshepperson/stubr
