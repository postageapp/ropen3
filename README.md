# ROpen3

Adds [`rbenv`](https://github.com/sstephenson/rbenv) compatibility to the
`Open3` suite of process tools for easier instantiation of alternate Ruby
versions from a Ruby parent process.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'ropen3'
```

And then execute:

```shell
bundle install
```

Or install it yourself as:

```gem
gem install ropen3
```

## Usage

To use ROpen3, establish the required version and `Gemfile` parameters, then
issue one or more `popen3` operations:

```ruby
ro = ROpen3.new(version: '2.3.3')

ro.popen3('gem env') do |_sin, sout, serr, proc|
  print sout.read
end
```

This can also be done using a block style:

```ruby
ROpen3.new(version: '2.3.3') do |ro|
  ro.popen3('gem env') do |_sin, sout, serr, proc|
    print sout.read
  end
end
```

All [`popen3`](https://rubyapi.org/3.0/o/open3#method-i-popen3) options,
including environment variable overrides, are supported as these are forwarded
through:

```ruby
ROpen3.new(version: '2.3.3') do |ro|
  ro.popen3({ 'VERBOSE' => '1' }, 'example', binmode: true) do |_sin, sout, serr, proc|
    print sout.read
  end
end
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then,
run `rake spec` to run the tests. You can also run `bin/console` for an
interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then
run `bundle exec rake release`, which will create a git tag for the version,
push git commits and the created tag, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at
https://github.com/postageapp/ropen3. This project is intended to be
a safe, welcoming space for collaboration, and contributors are expected to
adhere to the [code of conduct](https://github.com/tadman/rbenv_popen3/blob/master/CODE_OF_CONDUCT.md).

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the ROpen3 project's codebases, issue trackers,
chat rooms and mailing lists is expected to follow the
[code of conduct](https://github.com/tadman/rbenv_popen3/blob/master/CODE_OF_CONDUCT.md).
