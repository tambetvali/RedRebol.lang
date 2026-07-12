# Here are the basic answers from CoPilot:

##### tio.run - basic example runner (online non-auth interpreter)

Tio, which in Laegna reads theorem input-output:
- Run samples online, get output
- https://tio.run/#red

  Try this:
  ```red
  Red[]

  print "Hello from Red!"
  view [text "Hello from Red/View"]
  ```

  It runs the console part, fails UI as expected (so we can easily run console if UI not available):
  ```console
  Hello from Red!
  *** Script Error: view has no value
  *** Where: ???
  ```

  So we remove UI:
  ```red
  Red[]
  print "OK"
  ```

  We don't remove console:
  ```red
  Red[]
  view [text "Hi"]
  ```

  Removing UI, tio is just OK:
  ```console
  OK
  ```

  That's what we got out of it.
- Let's try Rebol with same script, same environment: https://tio.run/#rebol, https://tio.run/#rebol3 - switch languages to actually switch languages in my case, find rebol
 
  ```rebol
  Rebol[]
  
  print "Hello from Rebol!"
  view layout [
      text "Hello from Rebol/View"
  ]
  ```

  Rebol, as well, is able to greet you from console before it gets the error of no UI.

  ```console
  Hello from Rebol!
  ** Script Error: view has no value
  ** Near: view layout [
      text "Hello from Rebol/View"
  ]
  >>
  ```

  Rebol 3 is close after, *seems backward compatible*, altough *where is the error pointing*:

  ```console
  Hello from Rebol!
  ** Script error: view has no value
  ** Where: do either either either -apply-
  ** Near: do intern code
  
  >> 
  ```

  Remove UI:
  ```rebol
  Rebol[]
  print "OK"
  ```

  You have already seen this one, and you would see it twice with Rebol and Rebol3:

  ```console
  OK
  ```

  Leave only UI:
  ```rebol
  Rebol[]
  view layout [
      text "Hi"
  ]
  ```

  What you won't miss, is an error:
  ```console
  ** Script Error: view has no value
  ** Near: view layout [
      text "Hi"
  ]
  >>
  ```

  Or rebol3 version of it:
  ```console
  ** Script error: view has no value
  ** Where: do either either either -apply-
  ** Near: do intern code
  
  >> 
  ```

"Iteration 1" of ability is now done:
- We can already implement syntax, and test it.
  - It won't need UI.

We cannot run UI nor serve web. Let's go further with provisions and try the same code.

- 

# Can we use it online?

Well the name makes sense in terminology of "digital nomads", but this is not full mode: just enabling one to work online and offline as they want, without permanent station. You just eat what you get - in Barcelona they have Locutories, perhaps you use friend's computer or anything while it's away. It's not good idea if your app programming habit needs full installation of your customized environment.

I asked CoPilot the second day, answered the "how to ask precisely what I want":

> Let's try again, with my question very precise and including that we didn't find much by more specific criteria:
> - Free.
> - 24/7 free.
> - Might have limited additional resources, but paid resources must be added value such as GBs and TBs, not essentials.
> - Has console - Red programming requires at least this.
> - Has visual IDE or editor, which does not lag on long files preferrably.
> - Allows to program in Red (essential), maybe Rebol (optional, plus).
> - Preferrably: able to serve the web page from it's internal server address, and very optionally it's "Console" could become tunnel and allow running some IDE: the latter, rather, is probably that I show the IDE program on web, and only compile it for IDE if downloading as application - I think it's "portability" should enable this as core function of the semantically good dialect.

