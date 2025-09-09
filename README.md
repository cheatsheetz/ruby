# Ruby Cheat Sheet

Comprehensive reference for Ruby programming language covering syntax, blocks, iterators, metaprogramming, and essential features for modern Ruby development.

---

## Table of Contents
- [Basic Syntax](#basic-syntax)
- [Variables and Data Types](#variables-and-data-types)
- [Control Structures](#control-structures)
- [Methods](#methods)
- [Blocks and Iterators](#blocks-and-iterators)
- [Classes and Objects](#classes-and-objects)
- [Modules and Mixins](#modules-and-mixins)
- [Exception Handling](#exception-handling)
- [File Operations](#file-operations)
- [Regular Expressions](#regular-expressions)
- [Metaprogramming](#metaprogramming)
- [Standard Library](#standard-library)

---

## Basic Syntax

| Feature | Syntax | Example |
|---------|--------|---------|
| Print Output | `puts`, `print`, `p` | `puts "Hello World"` |
| Comments | `# single line` or `=begin multi =end` | `# This is a comment` |
| String Interpolation | `"#{expression}"` | `"Hello #{name}"` |
| Method Call | `object.method` or `method(args)` | `"hello".upcase` |
| Assignment | `variable = value` | `name = "Ruby"` |
| Constants | `CONSTANT_NAME` | `PI = 3.14159` |

### Basic Program Structure
```ruby
#!/usr/bin/env ruby

# This is a comment
puts "Hello, World!"

# String interpolation
name = "Ruby"
puts "Hello, #{name}!"
```

## Variables and Data Types

### Variable Types
```ruby
# Local variables (lowercase or _)
local_var = "local"
_private = "underscore"

# Instance variables (@)
class MyClass
  def initialize
    @instance_var = "instance"
  end
end

# Class variables (@@)
class MyClass
  @@class_var = "class"
end

# Global variables ($)
$global_var = "global"

# Constants (UPPERCASE)
CONSTANT = "constant value"
PI = 3.14159
```

### Data Types
```ruby
# Numbers
integer = 42
float = 3.14
big_number = 1_000_000
scientific = 1.23e4
binary = 0b1010
octal = 0755
hex = 0xFF

# Strings
single_quote = 'Hello'
double_quote = "World"
multiline = <<~EOF
  This is a multiline string
  with indentation handled
EOF

# Symbols (immutable strings)
symbol = :name
symbol_with_spaces = :"first name"

# Booleans
true_val = true
false_val = false
nil_val = nil

# Arrays
array = [1, 2, 3, 4, 5]
mixed_array = [1, "two", :three, 4.0]
words = %w[apple banana cherry]  # Array of strings
symbols = %i[red green blue]     # Array of symbols

# Hashes
hash = { "name" => "John", "age" => 30 }
symbol_hash = { name: "John", age: 30 }  # Symbol keys shorthand
mixed_hash = { :name => "John", "age" => 30 }

# Ranges
inclusive_range = 1..10    # 1 to 10 (inclusive)
exclusive_range = 1...10   # 1 to 9 (exclusive)
letter_range = 'a'..'z'
```

### Type Checking and Conversion
```ruby
# Type checking
42.class                    # Integer
"hello".class               # String
:symbol.class               # Symbol
[1, 2, 3].class            # Array

42.is_a?(Integer)           # true
"hello".is_a?(String)       # true

# Type conversion
"123".to_i                  # 123
123.to_s                    # "123"
"3.14".to_f                 # 3.14
"hello".to_sym              # :hello
:hello.to_s                 # "hello"
[1, 2, 3].join(",")         # "1,2,3"
"1,2,3".split(",")          # ["1", "2", "3"]
```

## Control Structures

### Conditional Statements
```ruby
# if/elsif/else
if age >= 18
  puts "Adult"
elsif age >= 13
  puts "Teenager"
else
  puts "Child"
end

# Inline if (modifier)
puts "Adult" if age >= 18

# unless (opposite of if)
unless logged_in
  puts "Please log in"
end

# Ternary operator
status = age >= 18 ? "Adult" : "Minor"

# case/when
grade = "A"
case grade
when "A", "A+"
  puts "Excellent!"
when "B", "B+"
  puts "Good job!"
when "C"
  puts "Average"
when "D", "F"
  puts "Need improvement"
else
  puts "Invalid grade"
end

# case with ranges
score = 85
case score
when 90..100
  puts "A"
when 80..89
  puts "B"
when 70..79
  puts "C"
else
  puts "F"
end

# Spaceship operator
result = a <=> b  # Returns -1, 0, or 1
```

### Loops
```ruby
# while loop
i = 0
while i < 5
  puts i
  i += 1
end

# until loop (opposite of while)
i = 0
until i >= 5
  puts i
  i += 1
end

# for loop (rarely used)
for i in 1..5
  puts i
end

# loop with break
loop do
  puts "Infinite loop"
  break if some_condition
end

# next (similar to continue)
(1..10).each do |i|
  next if i.even?
  puts i  # Only prints odd numbers
end

# redo (restart current iteration)
attempts = 0
loop do
  attempts += 1
  puts "Attempt #{attempts}"
  redo if attempts < 3 && !success
  break
end
```

## Methods

### Method Definition
```ruby
# Basic method
def greet(name)
  "Hello, #{name}!"
end

# Method with default parameters
def greet_with_default(name = "World")
  "Hello, #{name}!"
end

# Method with multiple parameters
def add(a, b)
  a + b
end

# Method with splat operator (variable args)
def sum(*numbers)
  numbers.sum
end

# Method with keyword arguments
def create_user(name:, email:, age: 18)
  { name: name, email: email, age: age }
end

# Calling with keyword arguments
user = create_user(name: "John", email: "john@example.com")

# Method with double splat (keyword args)
def process_options(**options)
  options.each { |key, value| puts "#{key}: #{value}" }
end

process_options(format: "json", verbose: true)

# Method with block parameter
def with_timing(&block)
  start = Time.now
  result = block.call
  finish = Time.now
  puts "Took #{finish - start} seconds"
  result
end

with_timing { sleep(1) }

# Implicit return (last expression is returned)
def multiply(a, b)
  a * b  # This is automatically returned
end

# Explicit return
def divide(a, b)
  return "Cannot divide by zero" if b == 0
  a / b
end

# Method aliases
alias plus add
alias :goodbye :greet

# Method visibility
class Example
  def public_method
    "Anyone can call this"
  end
  
  private
  
  def private_method
    "Only callable within the class"
  end
  
  protected
  
  def protected_method
    "Callable by instances of this class or subclasses"
  end
end
```

## Blocks and Iterators

### Blocks
```ruby
# Block with {}
[1, 2, 3].each { |n| puts n }

# Block with do..end
[1, 2, 3].each do |n|
  puts n * 2
end

# yield in methods
def three_times
  yield(1)
  yield(2)
  yield(3)
end

three_times { |num| puts "Number: #{num}" }

# Block with parameters
def with_index
  ["a", "b", "c"].each_with_index do |item, index|
    yield(item, index)
  end
end

with_index { |item, i| puts "#{i}: #{item}" }

# block_given?
def maybe_yield
  if block_given?
    yield("Hello")
  else
    puts "No block provided"
  end
end

# Proc objects
my_proc = Proc.new { |x| puts x * 2 }
my_proc.call(5)  # 10

# Lambda
my_lambda = lambda { |x| puts x * 2 }
my_lambda.call(5)  # 10

# Stabby lambda syntax
square = ->(x) { x * x }
puts square.call(4)  # 16

# Difference between Proc and Lambda
# Lambda checks argument count, Proc doesn't
# return in Lambda returns from lambda, return in Proc returns from enclosing method
```

### Common Iterators
```ruby
# each
[1, 2, 3].each { |n| puts n }

# map/collect (transforms elements)
doubled = [1, 2, 3].map { |n| n * 2 }  # [2, 4, 6]
names = users.map(&:name)  # Extract names using symbol to proc

# select/filter
evens = [1, 2, 3, 4, 5].select { |n| n.even? }  # [2, 4]

# reject (opposite of select)
odds = [1, 2, 3, 4, 5].reject { |n| n.even? }  # [1, 3, 5]

# find/detect (returns first match)
first_even = [1, 2, 3, 4, 5].find { |n| n.even? }  # 2

# reduce/inject (accumulator)
sum = [1, 2, 3, 4, 5].reduce(0) { |acc, n| acc + n }  # 15
sum = [1, 2, 3, 4, 5].reduce(:+)  # 15 (using symbol)

# any?/all?
has_evens = [1, 2, 3].any?(&:even?)   # true
all_positive = [1, 2, 3].all? { |n| n > 0 }  # true

# times
5.times { |i| puts "Iteration #{i}" }

# upto/downto
1.upto(5) { |i| puts i }      # 1, 2, 3, 4, 5
5.downto(1) { |i| puts i }    # 5, 4, 3, 2, 1

# step
0.step(10, 2) { |i| puts i }  # 0, 2, 4, 6, 8, 10
```

## Classes and Objects

### Class Definition
```ruby
class Person
  # Class variable
  @@count = 0
  
  # attr_* methods create getters/setters
  attr_reader :name      # Read only
  attr_writer :age       # Write only
  attr_accessor :email   # Read and write
  
  def initialize(name, age)
    @name = name
    @age = age
    @@count += 1
  end
  
  # Instance method
  def introduce
    "Hi, I'm #{@name} and I'm #{@age} years old"
  end
  
  # Class method
  def self.count
    @@count
  end
  
  # Another way to define class methods
  class << self
    def reset_count
      @@count = 0
    end
  end
  
  # Private methods
  private
  
  def secret_method
    "This is private"
  end
end

# Creating instances
person = Person.new("Alice", 30)
puts person.introduce
puts Person.count
```

### Inheritance
```ruby
class Animal
  attr_accessor :name
  
  def initialize(name)
    @name = name
  end
  
  def speak
    "The animal makes a sound"
  end
end

class Dog < Animal
  def initialize(name, breed)
    super(name)  # Call parent constructor
    @breed = breed
  end
  
  def speak
    "#{@name} barks!"
  end
  
  def fetch
    "#{@name} fetches the ball"
  end
end

# Usage
dog = Dog.new("Buddy", "Golden Retriever")
puts dog.speak   # "Buddy barks!"
puts dog.fetch   # "Buddy fetches the ball"
```

### Class Variables and Methods
```ruby
class BankAccount
  @@interest_rate = 0.05
  
  attr_reader :balance, :account_number
  
  def initialize(account_number, initial_balance = 0)
    @account_number = account_number
    @balance = initial_balance
  end
  
  def deposit(amount)
    @balance += amount
  end
  
  def withdraw(amount)
    if amount <= @balance
      @balance -= amount
    else
      puts "Insufficient funds"
    end
  end
  
  def apply_interest
    @balance *= (1 + @@interest_rate)
  end
  
  # Class method to get interest rate
  def self.interest_rate
    @@interest_rate
  end
  
  # Class method to set interest rate
  def self.interest_rate=(rate)
    @@interest_rate = rate
  end
end

account = BankAccount.new("12345", 1000)
puts BankAccount.interest_rate  # 0.05
```

## Modules and Mixins

### Module Definition
```ruby
module Greetings
  def say_hello
    "Hello!"
  end
  
  def say_goodbye
    "Goodbye!"
  end
  
  # Module method
  def self.formal_greeting
    "Good day to you!"
  end
end

# Include module in class
class Person
  include Greetings
  
  attr_accessor :name
  
  def initialize(name)
    @name = name
  end
end

person = Person.new("Alice")
puts person.say_hello  # "Hello!"
puts Greetings.formal_greeting  # "Good day to you!"
```

### Mixins and Namespacing
```ruby
# Module as namespace
module Math
  PI = 3.14159
  
  def self.circle_area(radius)
    PI * radius * radius
  end
  
  class Calculator
    def add(a, b)
      a + b
    end
  end
end

puts Math::PI  # 3.14159
puts Math.circle_area(5)
calc = Math::Calculator.new

# Enumerable module
class TodoList
  include Enumerable
  
  def initialize
    @items = []
  end
  
  def add_item(item)
    @items << item
  end
  
  def each
    @items.each { |item| yield(item) }
  end
end

todo = TodoList.new
todo.add_item("Buy milk")
todo.add_item("Walk dog")

# Now we can use Enumerable methods
todo.map(&:upcase)
todo.select { |item| item.include?("milk") }

# Comparable module
class Version
  include Comparable
  
  attr_reader :version
  
  def initialize(version)
    @version = version
  end
  
  def <=>(other)
    version <=> other.version
  end
end

v1 = Version.new("1.0.0")
v2 = Version.new("2.0.0")
puts v1 < v2  # true
```

### extend vs include
```ruby
module Greetings
  def hello
    "Hello!"
  end
end

class Person
  extend Greetings   # Adds module methods as class methods
end

class Animal
  include Greetings  # Adds module methods as instance methods
end

puts Person.hello    # "Hello!" (class method)
puts Animal.new.hello # "Hello!" (instance method)
```

## Exception Handling

### Basic Exception Handling
```ruby
begin
  # Code that might raise an exception
  result = 10 / 0
rescue ZeroDivisionError => e
  puts "Cannot divide by zero: #{e.message}"
rescue StandardError => e
  puts "An error occurred: #{e.message}"
else
  puts "No exceptions occurred"
ensure
  puts "This always runs"
end

# Inline rescue
result = 10 / 0 rescue "Error occurred"

# raise exceptions
def validate_age(age)
  raise ArgumentError, "Age must be positive" if age < 0
  raise ArgumentError, "Age must be reasonable" if age > 150
end

begin
  validate_age(-5)
rescue ArgumentError => e
  puts "Invalid age: #{e.message}"
end
```

### Custom Exceptions
```ruby
class CustomError < StandardError
  def initialize(message = "A custom error occurred")
    super(message)
  end
end

class ValidationError < StandardError
  attr_reader :field
  
  def initialize(field, message)
    @field = field
    super("#{field}: #{message}")
  end
end

begin
  raise ValidationError.new("email", "is required")
rescue ValidationError => e
  puts "Validation failed for #{e.field}: #{e.message}"
end

# retry mechanism
attempts = 0
begin
  attempts += 1
  puts "Attempt #{attempts}"
  raise "Random error" if rand < 0.7
  puts "Success!"
rescue => e
  retry if attempts < 3
  puts "Failed after 3 attempts"
end
```

## File Operations

### File Reading and Writing
```ruby
# Read entire file
content = File.read("file.txt")

# Read file line by line
File.readlines("file.txt").each do |line|
  puts line
end

# Write to file
File.write("output.txt", "Hello, World!")

# Append to file
File.open("log.txt", "a") do |file|
  file.puts "Log entry: #{Time.now}"
end

# File operations with block (automatically closes)
File.open("data.txt", "r") do |file|
  while line = file.gets
    puts line
  end
end

# Check file existence and properties
if File.exist?("config.yml")
  puts "File exists"
  puts "Size: #{File.size('config.yml')} bytes"
  puts "Modified: #{File.mtime('config.yml')}"
end

# Directory operations
Dir.mkdir("new_folder") unless Dir.exist?("new_folder")

Dir.glob("*.rb").each do |ruby_file|
  puts "Ruby file: #{ruby_file}"
end

Dir.foreach(".") do |item|
  next if item == "." || item == ".."
  puts item
end

# File path operations
require 'pathname'

path = Pathname.new("/usr/local/bin/ruby")
puts path.dirname   # "/usr/local/bin"
puts path.basename  # "ruby"
puts path.extname   # ""

# File utilities
require 'fileutils'

FileUtils.cp("source.txt", "backup.txt")
FileUtils.mv("old_name.txt", "new_name.txt")
FileUtils.rm("temp_file.txt")
FileUtils.mkdir_p("deeply/nested/directory")
```

## Regular Expressions

### Pattern Matching
```ruby
# Basic regex
pattern = /hello/
text = "hello world"
puts text =~ pattern    # Returns position (0) or nil
puts text.match(pattern) # Returns MatchData object

# Case insensitive
pattern = /hello/i
puts "Hello World" =~ pattern  # 0

# String interpolation in regex
name = "John"
pattern = /#{name}/
puts "Hello John" =~ pattern

# Common regex methods
text = "The year 2023 was great"

# match
match = text.match(/\d{4}/)
puts match[0] if match  # "2023"

# scan (find all matches)
numbers = text.scan(/\d+/)
puts numbers  # ["2023"]

# gsub (global substitution)
new_text = text.gsub(/\d{4}/, "2024")
puts new_text  # "The year 2024 was great"

# split with regex
parts = "apple,banana;cherry:date".split(/[,;:]/)
puts parts  # ["apple", "banana", "cherry", "date"]

# Named captures
email = "user@example.com"
match = email.match(/(?<username>\w+)@(?<domain>[\w.]+)/)
if match
  puts "Username: #{match[:username]}"  # user
  puts "Domain: #{match[:domain]}"      # example.com
end
```

### Regex Patterns
```ruby
# Character classes
/[abc]/      # a, b, or c
/[a-z]/      # Any lowercase letter
/[A-Z]/      # Any uppercase letter
/[0-9]/      # Any digit
/[^abc]/     # Not a, b, or c

# Predefined character classes
/\d/         # Digit [0-9]
/\D/         # Non-digit
/\w/         # Word character [a-zA-Z0-9_]
/\W/         # Non-word character
/\s/         # Whitespace
/\S/         # Non-whitespace

# Quantifiers
/a*/         # Zero or more a's
/a+/         # One or more a's
/a?/         # Zero or one a
/a{3}/       # Exactly 3 a's
/a{2,5}/     # 2 to 5 a's
/a{2,}/      # 2 or more a's

# Anchors
/^hello/     # Start of string
/world$/     # End of string
/\bhello\b/  # Word boundary

# Groups
/(abc)+/     # Group
/(?:abc)+/   # Non-capturing group
/(?<name>abc)/ # Named group

# Validation examples
email_regex = /\A[\w+\-.]+@[a-z\d\-]+(\.[a-z\d\-]+)*\.[a-z]+\z/i
phone_regex = /\A\d{3}-\d{3}-\d{4}\z/
url_regex = /\Ahttps?:\/\/[\S]+\z/

def valid_email?(email)
  !!(email =~ email_regex)
end
```

## Metaprogramming

### Dynamic Method Definition
```ruby
class DynamicClass
  # define_method
  define_method :dynamic_hello do |name|
    "Hello, #{name}!"
  end
  
  # Dynamic method creation
  %w[get set delete].each do |action|
    define_method "#{action}_item" do |item|
      "#{action.capitalize}ting #{item}"
    end
  end
end

obj = DynamicClass.new
puts obj.dynamic_hello("World")  # "Hello, World!"
puts obj.get_item("data")        # "Getting data"

# method_missing
class FlexibleClass
  def initialize
    @attributes = {}
  end
  
  def method_missing(method_name, *args, &block)
    if method_name.to_s.end_with?('=')
      # Setter
      attribute = method_name.to_s.chomp('=')
      @attributes[attribute] = args.first
    elsif @attributes.key?(method_name.to_s)
      # Getter
      @attributes[method_name.to_s]
    else
      super
    end
  end
  
  def respond_to_missing?(method_name, include_private = false)
    method_name.to_s.end_with?('=') || 
    @attributes.key?(method_name.to_s) || 
    super
  end
end

obj = FlexibleClass.new
obj.name = "Ruby"
puts obj.name  # "Ruby"
```

### Class and Module Manipulation
```ruby
# attr_* methods are actually metaprogramming
class Person
  # This creates getter and setter methods
  attr_accessor :name, :age
  
  # Equivalent to:
  # def name
  #   @name
  # end
  # 
  # def name=(value)
  #   @name = value
  # end
end

# Class variables and methods at runtime
class DynamicMethods
  # Class instance variable
  @class_data = {}
  
  def self.create_accessor(name)
    # Create getter
    define_method name do
      instance_variable_get("@#{name}")
    end
    
    # Create setter
    define_method "#{name}=" do |value|
      instance_variable_set("@#{name}", value)
    end
  end
  
  def self.class_data
    @class_data
  end
end

DynamicMethods.create_accessor(:email)
obj = DynamicMethods.new
obj.email = "test@example.com"
puts obj.email

# Module extension
module Trackable
  def self.included(base)
    base.extend(ClassMethods)
    base.class_eval do
      attr_accessor :created_at
      after_initialize :set_created_at
    end
  end
  
  module ClassMethods
    def track_creation
      puts "#{self} instances are being tracked"
    end
  end
  
  private
  
  def set_created_at
    @created_at = Time.now
  end
end

class TrackedClass
  include Trackable
  
  def initialize
    after_initialize if respond_to?(:after_initialize, true)
  end
  
  private
  
  def after_initialize
    # Hook for initialization
  end
end
```

### eval and instance_eval
```ruby
# eval - evaluates string as Ruby code
code = "2 + 2"
result = eval(code)  # 4

# instance_eval - evaluates in context of an object
class Person
  def initialize(name)
    @name = name
  end
end

person = Person.new("Alice")
person.instance_eval do
  puts @name  # Access private instance variable
  def greeting
    "Hello from #{@name}"
  end
end

puts person.greeting  # "Hello from Alice"

# class_eval/module_eval - evaluates in context of class/module
String.class_eval do
  def palindrome?
    self == self.reverse
  end
end

puts "radar".palindrome?  # true

# Safer alternatives: instance_exec, class_exec
person.instance_exec("World") do |greeting|
  puts "#{@name} says hello to #{greeting}"
end
```

## Standard Library

### Common Standard Library Classes
```ruby
# Time and Date
require 'time'
require 'date'

now = Time.now
puts now.strftime("%Y-%m-%d %H:%M:%S")

date = Date.today
puts date.strftime("%B %d, %Y")

# JSON
require 'json'

hash = { name: "John", age: 30 }
json_string = hash.to_json
parsed_hash = JSON.parse(json_string)

# URI
require 'uri'
require 'net/http'

uri = URI("https://api.example.com/users")
response = Net::HTTP.get_response(uri)
puts response.body if response.is_a?(Net::HTTPSuccess)

# CSV
require 'csv'

# Write CSV
CSV.open("data.csv", "w") do |csv|
  csv << ["Name", "Age", "City"]
  csv << ["Alice", 30, "New York"]
  csv << ["Bob", 25, "Los Angeles"]
end

# Read CSV
CSV.foreach("data.csv", headers: true) do |row|
  puts "#{row['Name']} is #{row['Age']} years old"
end

# Base64
require 'base64'

encoded = Base64.encode64("Hello World")
decoded = Base64.decode64(encoded)

# Digest (hashing)
require 'digest'

sha256 = Digest::SHA256.hexdigest("password")
md5 = Digest::MD5.hexdigest("data")

# SecureRandom
require 'securerandom'

uuid = SecureRandom.uuid
random_hex = SecureRandom.hex(16)
random_base64 = SecureRandom.base64(16)

# Benchmark
require 'benchmark'

time = Benchmark.measure do
  1000000.times { "hello".upcase }
end
puts time

# Set
require 'set'

set = Set.new([1, 2, 3, 3, 4])  # [1, 2, 3, 4] (duplicates removed)
set.add(5)
set.delete(1)
puts set.include?(3)  # true

# OpenStruct
require 'ostruct'

person = OpenStruct.new(name: "Alice", age: 30)
person.city = "New York"
puts person.name  # "Alice"
```

---

## Resources
- [Ruby Official Documentation](https://ruby-doc.org/)
- [Ruby Style Guide](https://github.com/rubocop/ruby-style-guide)
- [Ruby on Rails Guides](https://guides.rubyonrails.org/)
- [RubyGems](https://rubygems.org/)
- [The Ruby Programming Language Book](https://www.oreilly.com/library/view/the-ruby-programming/9780596516178/)

---
*Originally compiled from various sources. Contributions welcome!*