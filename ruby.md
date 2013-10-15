* rake参数
```ruby
task :test, :p1 do |t, args|
  puts args[:p1]
end
rake test["test"]  # -> "test"
```

更好的方式
`$ ver=20130101 rake test`
```ruby
ver = ENV['ver'] # -> '20130101'
```

* 更新vagrant 虚拟机中的vbox guest 版本
`gem install vagrant-vbguest`

* 多行注释
```ruby
=begin
def a
  puts 'a'
end
=end
```

* Proc.new vs Lambda in ruby
```ruby
def foo
  f = Proc.new { return "return from foo from inside proc" }
  f.call # control leaves foo here
  return "return from foo" 
end

def bar
  f = lambda { return "return from lambda" }
  f.call # control does not leave bar here
  return "return from bar" 
end

puts foo # prints "return from foo from inside proc" 
puts bar # prints "return from bar" 
```

* Lazy Enumerator
`(0..Float::INFINITY).lazy.map{|i| ((-1) ** i) / (2*i + 1).to_f}.take(655360).reduce(:+) * 4`

* inject
```ruby
def fib(n)
  (0..n).inject([1,0]) { |(a,b), _| [b, a+b] }[0]
end
```
[1,0]

* FileUtil
```ruby
FileUtils.rm_rf '/tmp/home'
FileUtils.mkdir '/tmp/home'
```

* nokogiri
```ruby
page = Nokogiri::HTML(open(PAGE_URL))
news_links = page.css("a").select{|link| link['data-category'] == "news"}
news_links.each{|link| puts link['href'] }
page.css('p').css("a[data-category=news]").css("strong")
```
