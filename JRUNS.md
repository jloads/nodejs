## Przyklad

przyklad jak mozna wykorzystac zapis podobny do streamowania/routowania

    
    file/http -> DOM-xpath -> Javascript (local function)/ (external file)


Rozwiazanie pozwala na kontrolowanie kazdego elemetnu
pozwalajac na uruchomienie w czasie, gdy wszystko juz zostalo zaladowane
ograniczajac skutki niezaladowanych plikow/funkcji/elementow DOM

# Commands
    
+ from (source)
+ to (source)
+ by (function for processing between)
+ as (datamodel to use)
+ sort (up|date|time)
+ filter (xpath|file|exp)
+ msg(info|warning|error|log)
+ limit (10)


# Graph
reprezentacja graifczna tych zapytan w svg

# Local function

JS-script

    from("https://get.jloads.com/users.csv").to("table#users").by("LoadUsers");
  
  
JSON-config

    {  
      "from: "https://get.jloads.com/users.csv",
      "to": "table#users",
      "by": "LoadUsers"
    }
        
        
        
# External function

JS-script

    from("https://get.jloads.com/users.csv").to("table#users").by("https://get.jloads.com/load_users.js");
  
  
JSON-config

    {  
      "from: "https://get.jloads.com/users.csv",
      "to": "table#users",
      "by": "https://get.jloads.com/load_users.js"
    }
    
    
# more

      from("file:c:\dir")
        .filter()
        .xpath(expression)
        .to("jms :aQueue");
        
        
      from("file:data/inbox")
        .filter()
        .xpath("/order[not(@test)]")
        .to("jms:queue:order")


SpringRouteBuilder
https://access.redhat.com/node/2583501/fluent%20builders/Fluent%20Builders


# Multiple independent inputs

The simplest way to specify multiple inputs is using the multi-argument form of the from() DSL command, for example:

    from("URI1", "URI2", "URI3").to("DestinationUri");

Or you can use the following equivalent syntax:

    from("URI1").from("URI2").from("URI3").to("DestinationUri");

In both of these examples, exchanges from each of the input endpoints, URI1, URI2, and URI3, are processed independently of each other and in separate threads. In fact, you can think of the preceding route as being equivalent to the following three separate routes:

    from("URI1").to("DestinationUri");
    from("URI2").to("DestinationUri");
    from("URI3").to("DestinationUri");


# layers


## Meta Layer

+ name
+ version
+ description
+ url docs
+ url git


## Stream / Config layer

    from -> to 
                -> by 
                -> as
                -> filter 
                -> sort
                

## Exception / Live Management layer                

+ not executed
+ executed, Failed
+ queue
    + config    
    + element
    + source: from/to
    + sorting
    + filtering
    + assigment
    + function


## Information / Message / log Layer
    
+ info
+ warning
+ error



## Code for layers

    var in = Array()
    in.config
        + from
        + to 
        + by 
        + as
        + filter 
        + sort
        
    in.meta
        + name
        + version
        + description
        
    out = new jRuns(in);
    
    out.queue
        .first
        .end
        .current
        .next
        .all
        
    out.log
        .info
        .warning
        .error
        
    out.exception
        .exit
        .run


## Uzycie w kodzie
moze byc uzupelniany in.config - jako objekt json

Moze byc jako objekt po wykonaniu wykorzytsany do dalszego przetwarzania

    out2 = new jRuns(out.all);
    
## Example 1

    in.config
        + from
    
    in1 = in
    in1.config
        + to 
        + by 
        
    in2 = in
    in2.config
        + to 
        + by 
        
    out = new jRuns(in);
    
