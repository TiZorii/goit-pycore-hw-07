## Home task. Working with Files and Modular System

#### Task Description

**Task 1**

First, let's add additional functionality to the classes from the previous homework:

- Add a field named **`birthday`** for the date of birth in the **`Record`** class. This field should be of type **`Birthday`**. This field is optional but can only occur once.

```
class Birthday(Field):
def **init**(self, value):
try: # Add data correctness check # and convert the string to a datetime object
except ValueError:
raise ValueError("Invalid date format. Use DD.MM.YYYY")

class Record:
def **init**(self, name):
self.name = Name(name)
self.phones = []
self.birthday = None
```

- Add functionality to work with **`Birthday`** in the **`Record`** class, namely a function named **`add_birthday`**, which adds the birthday to the contact.
- Add validation for the provided values for the **`Phone`** and **`Birthday`** fields.
- Add and adapt to the **`AddressBook`** class our function from the fourth homework, week 3, **`get_upcoming_birthdays`**, which returns a list of users who need to be greeted for their birthdays in the next week.

Now, your bot should specifically work with the functionality of the **`AddressBook`** class. This means that instead of the `contacts` dictionary, we use `book = AddressBook()`.

**Task 2**

To implement the new functionality, also add handler functions with the following commands:

- **`add-birthday`** - adds the birthday in the format `DD.MM.YYYY` to the contact.
- **`show-birthday`** - displays the birthday of the contact.
- **`birthdays`** - returns a list of users who need to be greeted for their birthdays in the next week.

```
@input_error
def add_birthday(args, book):
    # implementation

@input_error
def show_birthday(args, book):
    # implementation

@input_error
def birthdays(args, book):
    # implementation
```

So in the end, our bot should support the following list of commands:

1. **`add`** **`[name] [phone]`**: Add a new contact with the name and phone number, or add a phone number to an existing contact.
2. **`change`** **`[name] [old phone] [new phone]`**: Change the phone number for the specified contact.
3. **`phone`** **`[name]`**: Show the phone numbers for the specified contact.
4. **`all`**: Show all contacts in the address book.
5. **`add-birthday`** **`[name] [birthdate]`**: Add a birthdate for the specified contact.
6. **`show-birthday`** **`[name]`**: Show the birthdate for the specified contact.
7. **`birthdays`**: Show the birthdays that will occur during the next week.
8. **`hello`**: Get a greeting from the bot.
9. **`close`** or **`exit`**: Close the program.

```
def main():
    book = AddressBook()
    print("Welcome to the assistant bot!")
    while True:
        user_input = input("Enter a command: ")
        command, *args = parse_input(user_input)

        if command in ["close", "exit"]:
            print("Good bye!")
            break

        elif command == "hello":
            print("How can I help you?")

        elif command == "add":
            # implementation

        elif command == "change":
            # implementation

        elif command == "phone":
            # implementation

        elif command == "all":
            # implementation

        elif command == "add-birthday":
            # implementation

        elif command == "show-birthday":
            # implementation

        elif command == "birthdays":
            # implementation

        else:
            print("Invalid command.")
```

For example, let's consider the implementation of the **`add`** **`[name] [phone]`** command. In the **`main`** function, we need to add handling for this command in the appropriate place:

```
elif command == "add":
print(add_contact(args, book))
```

The implementation of the **`add_contact`** function may look like this:

```
@input\*error
def add_contact(args, book: AddressBook):
name, phone, \*\* = args
record = book.find(name)
message = "Contact updated."
if record is None:
record = Record(name)
book.add_record(record)
message = "Contact added."
if phone:
record.add_phone(phone)
return message
```

Our **`add_contact`** function has two purposes - adding a new contact or updating the phone for an existing contact in the address book.

The parameters of the function are the **`args`** argument list and the address book **`book`**.

- First, the function unpacks the **`args`** list, obtaining the **`name`** and **`phone`** from the first two elements of the list. The rest of the arguments are ignored using **`\*\_`**. Then the **`find`** method of the **`book`** object performs a search for a record with the **`name`**. If a record with such a name exists, the method returns this record, otherwise it returns **`None`**.

- If the record is not found, then it is a new contact, and the function creates a new **`Record`** object with the **`name`** and adds it to the **`book`** by calling the **`add_record`** method. After adding a new record, the message variable is assigned the message `"Contact added"`. if the operation was successful.

- Then, regardless of whether the record was found or a new one was created, a phone number is added to this record using the **`add_phone`** method if it was provided. Finally, the function returns a message about the result of its work: `"Contact updated"`. if the contact was updated or `"Contact added"`. if the contact was added. To handle input errors and display the appropriate error message, we use the **`@input_error`** decorator.
