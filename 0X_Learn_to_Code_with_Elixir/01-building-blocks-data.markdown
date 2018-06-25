* What are data types and why do we care?
  * What's the purpose of programming?
  * ultimately a way to get a computer to make a decision for us, so that we don't have to spend brain power doing it
  * In order to get the computer to make decisions on our behalf, we have to help it understand our world. So that it can make decisions about our world.
  * Let's talk about some of the tools we have to represent our world

* Integers and Floats
  * Probably the most fundamental building block
  * Think: Banking Applications (balances), Games (Points, Scoreboards), Thermostats (Temp)
  * Basic operations with Integers and Floats
    * Addition, Subtraction, Division, Multiplication
    * Depositing money to a bank account
    * Withdrawing money from a bank account
    * Calculating how high a character jumps based on gravity
    * Calculating critical hit damage vs a zombie

* Strings
  * Another fundamental building block
  * Think: Twitter (tweets), WhatsApp (SMS)
  * Basic operations with Strings
    * Concatenation
    * Adding a greeting to a provided name on login

* Compound Data Types
  * Fundamental building blocks alone aren't sufficient for representing our world
  * We don't just want to describe a bank balance ($125), we want to describe an ACCOUNT
  * Map
    * An account has many attributes
      * owned by "Laura"
      * currently has $125
      * has an account number
      * has a routing number
    * So we can translate to something like
      %{
        "owner" => "Laura",
        "amount" => 125,
        "account_number" => 00005671,
        "routing" => 1894593882
      }

    * Maps allow you to describe a concept or an object with attributes
    * When describing a vehicle, you might talk about how many wheels it has, what type of propulsion it has, what color it is, what material it's made from, what its occupancy is, its name
    * When describing a building, you might talk about how many windows it has, what kind of insulation it has, what kind of roof it has, what color its paint is, what its last appraisal was, what type of foundation it has, where it's located (lat/long, neighborhood, city, state), who owns the title, when it was last purchased, how much property taxes are, how many bedrooms / bathrooms there are, how many sqft it has, etc.

    * Class exercise: how might we represent a transaction
      * First step, how do we describe a bank transaction
      * Transaction transfers money from one account to another account on a particular date
      * from account, to account, amount transferred, when transferred, transaction number
      * so might look like
        * %{
              "from" => 00005671,
              "to" => 00005672,
              "amount" => 20,
              "when" => "May 20, 2018",
              "transaction_number" => 12
            }
      * and then you might have another transaction like
        * %{
              "from" => 00005671,
              "to" => 00005673,
              "amount" => 25,
              "when" => "May 21, 2018",
              "transaction_number" => 13
            }

  * Lists
    * Older bank accounts don't have just one transaction, typically they have a whole history of transactions
    * You can represent a transaction history as a LIST of transactions
    * here's what a list might look like [ transaction, transaction, transaction ]
    * and this transaction list might exist on the account object:
    *  %{
          "owner" => "Laura",
          "amount" => 125,
          "account_number" => 00005671,
          "routing" => 1894593882,
          "transactions" => [ transaction, transaction, transaction ]
        }

  * lists are great because you can store anything in them
    * maybe you want a list of ElixirBridge attendees: ["Amy", "Bob", "Charlie", "Dana", ...]
    * maybe you want a list of Lotto numbers: [3, 6, 12, 15, 35, 51]
    * maybe you're doing some planning and want a list of Saturdays in 2018: [..., "June 23", "June 30", "July 7", ...]
    * an account has a list of transactions
    * a neighborhood has a list of houses
    * a state has a list of cities
    * a car has a list of wheels
    * a business has a list of employees, a list of products, a list of executives, a list of investors, a list of customers, a list of testimonials
    * an ikea furniture kit has a list of parts

* Variables
  * Point out that referring to large structs or large lists is cumbersome and painful
  * When constructing a list of transactions, you don't want to type out each transaction over and over again
  * You want to type out the first transaction once, and save it away for reference later
  * Then construct the next transaction and save it away for reference
  * `transaction_one = %{"from" => 000123, ...}`
  * `transaction_two = %{"from" => 000123, ...}`
  * Then when you build a list, you can refer to them by name, rather than by value
    * [ transaction_one, transaction_two, transaction_three ]
  * Maybe you want to name ^ this list your `transactions_list`
    * `transactions_list = [transaction_one, transaction_two, transaction_three]`
  * Then when you build your account, you can
    * `my_account = %{ "owner" => "Laura", ..., "transactions" => transaction_list }`

  * Variables are great because you can give names to anything
    * number_of_cars = 100
    * wheels_per_car = 4
    * my_city = "San Francisco"
    * my_state = "California"
    * my_account = %{ ... }

  * Then, just like we operated on numbers above, we can operate on variables:
    * number_of_cars * wheels_per_car
    * then save that off in a variable!
    * total_wheels = number_of_cars * wheels_per_car
  * And also with strings
    * my_city <> ", " <> my_state
    * then save that off in a variable!
    * my_location = my_city <> ", " <> my_state