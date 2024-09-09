#task 1
class BalanceModificationError(Exception):
    """Виняток, що сигналізує про заборону змінення балансу."""
    pass

class NonExistingPropertyError(Exception):
    """Виняток для доступу до неіснуючої властивості."""
    pass

class BalanceDescriptor:
    def __init__(self, initial_value=0):
        self._value = initial_value

    def __get__(self, instance, owner):
        print(f"Accessing balance: {self._value}")
        return self._value

    def __set__(self, instance, value):
        raise BalanceModificationError("Cannot modify balance directly.")

class Account:
    balance = BalanceDescriptor()

    def __init__(self, initial_balance=0):
        self.__dict__['_balance'] = initial_balance

    @property
    def balance(self):
        return self._balance

    def __setattr__(self, name, value):
        if name == 'balance':
            raise BalanceModificationError("Cannot modify balance directly.")
        print(f"Setting attribute {name} to {value}")
        super().__setattr__(name, value)

    def __getattr__(self, name):
        raise NonExistingPropertyError(f"Property '{name}' does not exist.")

account = Account(1000)

print(account.balance)

try:
    account.balance = 500
except BalanceModificationError as e:
    print(e)

try:
    print(account.non_existing_property)
except NonExistingPropertyError as e:
    print(e)
#task 2
class NameModificationError(Exception):
    """Виняток для сигналізації про заборону зміни імені."""
    pass

class User:
    def __init__(self, first_name, last_name):
        self.__dict__['_first_name'] = first_name
        self.__dict__['_last_name'] = last_name

    @property
    def first_name(self):
        print("Accessing first_name")
        return self._first_name

    @property
    def last_name(self):
        print("Accessing last_name")
        return self._last_name

    def __setattr__(self, name, value):
        if name in ['first_name', 'last_name']:
            raise NameModificationError(f"Cannot modify {name} directly.")
        if name == 'first_name' and not value.isalpha():
            raise ValueError("First name must contain only alphabetic characters.")
        if name == 'last_name' and not value.isalpha():
            raise ValueError("Last name must contain only alphabetic characters.")
        print(f"Setting attribute {name} to {value}")
        super().__setattr__(name, value)

    def __getattr__(self, name):
        raise NonExistingPropertyError(f"Property '{name}' does not exist.")

user = User("John", "Doe")

print(user.first_name)

try:
    user.first_name = "Jane123"
except (NameModificationError, ValueError) as e:
    print(e)

try:
    print(user.non_existing_property)
except NonExistingPropertyError as e:
    print(e)
#task 3
class DimensionModificationError(Exception):
    """Виняток для сигналізації про заборону зміни розмірів."""
    pass

class Rectangle:
    def __init__(self, width, height):
        if width <= 0 or height <= 0:
            raise ValueError("Dimensions must be positive numbers.")
        self.__dict__['_width'] = width
        self.__dict__['_height'] = height

    @property
    def width(self):
        print("Accessing width")
        return self._width

    @property
    def height(self):
        print("Accessing height")
        return self._height

    def __setattr__(self, name, value):
        if name in ['width', 'height']:
            raise DimensionModificationError(f"Cannot modify {name} directly.")
        if name in ['_width', '_height'] and value <= 0:
            raise ValueError(f"{name} must be a positive number.")
        print(f"Setting attribute {name} to {value}")
        super().__setattr__(name, value)

    def __getattr__(self, name):
        raise NonExistingPropertyError(f"Property '{name}' does not exist.")

    def update_dimensions(self, width=None, height=None):
        if width is not None:
            if width <= 0:
                raise ValueError("Width must be a positive number.")
            print(f"Updating width to {width}")
            self.__dict__['_width'] = width
        if height is not None:
            if height <= 0:
                raise ValueError("Height must be a positive number.")
            print(f"Updating height to {height}")
            self.__dict__['_height'] = height

    def area(self):
        print(f"Calculating area: {self.width} * {self.height}")
        return self.width * self.height

rectangle = Rectangle(10, 20)

print(rectangle.width)

try:
    rectangle.width = 30
except DimensionModificationError as e:
    print(e)

rectangle.update_dimensions(width=15, height=25)

print("Area:", rectangle.area())

try:
    print(rectangle.non_existing_property)
except NonExistingPropertyError as e:
    print(e)
