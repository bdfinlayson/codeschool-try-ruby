# codeschool-try-ruby
My notes from Codeschool's Try Ruby course at http://tryruby.org/

### Using `Dir[]`
So, what exactly is that `Dir.entries` method? Well, it's just a method, like the others you've seen. `Dir` has a collection of methods for checking out file directories, and entries is being called on the `Dir` variable. The entries method just lists everything in the directory you've indicated!

One other little thing we haven't really talked about quite yet: method arguments. A few are highlighted below.
`Dir.entries "/"` -- Anything listed after a method is considered an 'attachment'.

`print poem` -- See, `print` is just an ordinary method, while the poem is what got attached for printing.

`print "pre", "event", "ual", "ism"` -- This bit has several arguments! Ruby makes us use commas to distinguish between them.
Next up, we'll list just the text files in our root directory using a bracket notation. Remember how it searches?

Try: `Dir["/*.txt"]`

The `Dir[]` syntax is kind of like `entries`, but instead searches for files with wildcard characters.
Here, we see those square brackets again! Notice how they still mean, "I am looking for _____?"
`Dir["/*.txt"]` says to Ruby: "I am looking for any files which end with `.txt`." The asterisk indicates the "any file" part. Ruby then hands us every file that matches our request.

Alright, let's crack open this comics file, then! We'll use a new method to do it.
Here's the way: `print File.read("/comics.txt")`

### Moving Files
Alright, then! Now we can start to use files to store things. This is great because normally when we exit Ruby, all our variables will be gone. Ruby, by itself, forgets these things. But if we save things in files, we can read those files in future Ruby escapades.

Hey, and guess what? The /Home directory is yours now! I gave it to you! Am I generous or what?!
First thing we'll do is make a copy of the comics file and put in new folder called 'Home'.
To do that, you'll want to use a copying method called cp on a variable called FileUtils.
Use `FileUtils.cp('/comics.txt', '/Home/comics.txt')`

### Append To Files
To add your own comic to the list, let's open the file in append mode, which we indicate with the "a" parameter. This will allow us to put new stuff at the end of the file.

Start by entering this code: `File.open("/Home/comics.txt", "a") do |f|`
*this is a method that allows you to do things like add content to files for example*
`f << "Some Text and a url reference"`
`end`
Sweet! You've added that brand new comic to the end of the file. You can see for yourself, using the read method you saw earlier: `print File.read("/Home/comics.txt")`.

### Tracking Changes To Files
I wonder, what time was it when you changed your file? We can check that out.
Type: `File.mtime("/Home/comics.txt")`.
*this prints out a UTC formatted time YYY-MM-DD HH-MM-SS UTC*
*You can access a specific time with chaining*
`File.mtime("/Home/comics.txt").hour`


### Building Your Own Methods
Start building our new method with: 
`def load_comics( path )`
  `comics = {}`
  `File.foreach(path) do |line|`
    `name, url = line.split(': ')`
    `comics[name] = url.strip`
  `end`
  `comics`
`end`


`File.foreach` -- This method opens a file and hands each line of the file to the block. The line variable inside the do...end block took turns with each line in the file.

`split` -- A method for strings which breaks the string up into an array, removing the piece you pass in. An axe is laid on the colon and the line is chopped in half, giving us the data to be stored in url and name for each comic.

`strip` -- This quickie removes extra spaces around the url. Just in case.

