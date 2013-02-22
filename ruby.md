# ruby tips

## rake参数
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

## 更新vagrant 虚拟机中的vbox guest 版本
`gem install vagrant-vbguest`

## 多行注释
```ruby
=begin
def a
  puts 'a'
end
=end
```

