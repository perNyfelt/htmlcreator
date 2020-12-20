# Renjin html creator
Renjin R package to create html  

This package provides a simple way to create html content.
Here is an example:
```r
  library('se.alipsa:htmlcreator')

  html.add("<html><body>")
  html.add("<h2>A Sample report with a table and an image</h2>")
  html.add(
    barplot,
    table(mtcars$vs, mtcars$gear),
    main="Car Distribution by Gears and VS",
    col=c("darkblue","red")
  )
  html.add(mtcars)
  html.add("</html></body>")
  # save the html to a file
  outFile <- tempfile("plot", fileext = ".html")
  write(html.content(), outFile)
  print(paste("Wrote", outFile))
```
To be able to do this, add the dependency to your pom.xml as follows:
```xml
<dependency>
  <groupId>se.alipsa</groupId>
  <artifactId>htmlcreator</artifactId>
  <version>1.1</version>
</dependency>
```
As you can see, the mail method is the overloaded `html.add`. It can take
strings as parameters (which are treated as raw html),
a data.frame (which is converted into a html table), 
or a plot function (which converts the plot into an img tag)

Besides this, there is the html.clear() function which resets the 
underlying html object (clears the content).

html attributes can be set by passing setting the parameter `htmlattr` to a list of attribute, e.g:
```r
# add id anc class to a table:
html.add(mtcars, htmlattr=list(id="cardetails", class="table table-striped"))

# add alt attribute to an img:
html.add(
  barplot,
  table(mtcars$vs, mtcars$gear),
  main="Car Distribution by Gears and VS",
  col=c("darkblue","red"),
  htmlattr = list(alt="an mtcars plot")
)
```

It is also possible to use the underlying reference class (Html) and the specific
html creating methods directly. The underlying html creating methods are:
- html.table - converts a data.frame to a table
- html.img - converts a plot to an img
- html.imgFile - converts a file to an img
