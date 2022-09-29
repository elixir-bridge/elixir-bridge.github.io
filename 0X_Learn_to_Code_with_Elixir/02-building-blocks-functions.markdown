* With our DATA building blocks, we can construct a new world for the computer to operate in
* We can teach it about accounts, we can teach it about transactions
* We can teach it about cars, buildings, businesses, any other concrete object in the world, and even more abstract concepts

* But this world isn't interesting if nothing moves
* Twitter wouldn't be interesting unless you could CREATE tweets, or LIKE tweets, or RETWEET tweets
* Youtube wouldn't be interesting unless you could DOWNLOAD videos and WATCH them
* Google Calendar wouldn't be interesting unless you could SCHEDULE events, MOVE events, ADD locations, INVITE participants
* Gmail wouldn't be interesting unless you could DRAFT a new email, ADD recipients, CHANGE the email body, SEND the email, RECEIVE email
* Note that all the interesting things above involve a data building block (tweet, video, events, locations, participants, email, email addresses)
* They become interesting when they are given life

* We need a way to represent __action__ in our world


* Functions do 3 things
  * Accept some input
  * Do something
  * Return some output


* Elixir has already written some functions for you. Let's play around with them
  * String.capitalize("california")
    (takes "california" as input
      transforms it by capitalizing the first letter
      returns the transformed string)
  * String.length("how many letters?")
    (takes "how many letters?" as input
      counts the number of letters in the string, including spaces and question marks
      returns that number)
  * List.first(["Nancy", "Charles", "Wilfred"])
    (takes a list as input
      extracts the first item from the list
      returns that item)
  * List.delete(["my account", "their account", "your account", "my friend's account"], "your account")
    (takes a list as input
      removes the specified item from the list
      returns a shorter list without the specified item)
  * Map.get(account, "owner")
    (takes a map as input
      finds the "owner" key and extracts the corresponding value
      returns the value)
  * Map.put(account, "owner", "Jake")
    (takes a map as input
      transforms it by setting the "owner" to "Jake"
      returns the map)
  * Map.keys(account)
    (takes a map as input
      extracts a list of all the keys it can find in the map
      returns the list)

* Let's briefly point out the structure of the above functions:
  * Module.function_name(inputs, go, here)
  * What's a module? Just like files have folders, functions have modules. They're a way for you to organize your functions
    * Look at the functions above:
      * All the functions that operate on strings (capitalize, length) are in the String module
      * All the functions that operate on lists (first, delete) are in the List module
      * All the functions that operate on maps (get, put, keys) are in the Map module
    * As a side note, this lets use reuse function names:
      * Map.delete transforms a map by deleting a key
      * List.delete transforms a list by removing an item


* You might write a function to reschedule a calendar event
  * Inputs: the event to reschedule, when it should be rescheduled to
  * Do something: transform the event by saving the new time
  * Return the new event
  * CalendarEvent.move(event, "Mar 21, 2018")

* You might write a function to like a tweet
  * Inputs: tweet to be liked
  * Do something: add 1 to the # of likes the tweet has
  * Return the changed tweet
  * Tweet.like(tweet)

* You might write a function to add a recipient to your email draft
  * Inputs: unsent email, new recipient address
  * Do something: add the recipient address to the recipient list
  * Return the updated email
  * Email.add_recipient(email, "jose@elixirbridge.com")

* You might write a function to draft a new email
  * Inputs: nothing!
  * Do something: construct a bare bones email map with empty values
  * Return the new email draft
  * Email.new()


