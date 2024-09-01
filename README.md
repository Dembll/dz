#task 1
def sequence_generator(func, first_value, n):
    """
    Generator for a numerical sequence.

    :param func: User-defined function to get the next term in the sequence.
    :param first_value: The initial value (first term) of the sequence.
    :param n: The number of terms to generate.
    """
    value = first_value
    for _ in range(n):
        yield value
        value = func(value)


def next_term(value):
    """
    User function that defines the rule for generating the sequence.
    For example, progression: next term = previous term + 2.

    :param value: The previous term in the sequence.
    :return: The next term in the sequence.
    """
    return value + 2  # Example rule: each next term is 2 more than the previous one


gen = sequence_generator(next_term, 1, 10)  # Start with 1, generate 10 terms

for num in gen:
    print(num)
#task 2
def memoize_fibonacci():
    cache = {}

    def fibonacci(n):
        if n in cache:
            return cache[n]

        if n <= 1:
            return n

        cache[n] = fibonacci(n - 1) + fibonacci(n - 2)
        return cache[n]

    return fibonacci


fib_memoized = memoize_fibonacci()

n = 35
print(f"Fibonacci({n}) with memoization:", fib_memoized(n))
#Висновок:Функція з мемоізацією значно прискорює обчислення ряду Фібоначчі
#task 3
def apply_and_sum(numbers, func):
    return sum(func(num) for num in numbers)

def square(x):
    return x ** 2

numbers = [1, 2, 3, 4, 5]
result = apply_and_sum(numbers, square)
print(f"Sum of squares: {result}")
