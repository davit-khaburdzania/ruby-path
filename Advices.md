## Unable to install gems 
i was unable to install gems due to permition error so solution was to install ruby 2.1.2 using [rvm](https://rvm.io/)
```bash
curl -sSL https://get.rvm.io | bash -s stable
rvm install 2.1.2
rvm use 2.1.2 --default
```

## method visibility
protected and private keywords work differently then other languages: so if you mark method to be private you can invoke it only using implicit invocation inside of this class methods:

```ruby
class Person
  def test
    hello #this works / implicit invocation
    self.hello #this doesn't work / explicit invocation
  end

  private
  def hello
    puts "hello there"
  end
end

person = Person.new
person.test
```

you can also invoke parent private methods implicitly in child class:

```ruby
class Parent
  private
  def hello
    puts "hello i am parent "
  end
end

class Child < Parent
  def test
    hello #this works / implicit invocation
    self.hello #this doesn't work / explicit invocation
  end
end


child = Child.new
child.test
```

protected keyword works same way but you can call it using implicit invocation and explicit invocation too.

you can't call private or protected methods outside of class:
```ruby
class Person
  protected
  def hello_protected
    puts "hello i am protected"
  end

  private
  def hello_private
    puts "hello i am private"
  end
end

child = Person.new
#both raises error
child.hello_protected
child.hello_private
```

### Procs and Lambdas
one of differences between proc and lamda is that, if we define both with arguments when we call both proc will procceed and lambda will raise error 

```ruby
test = proc { |text| puts "#{text} --- proc" }
test2 = lambda { |text| puts "#{text}  ---  lambda" }

test.call() # this will work 
test2.call() # this will raise error, expected argument

```
