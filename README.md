# ReportQuery [WIP]

The idea of this gem is to generate the most optimal queries for report. Currently when table count increases in a project, it is really hard to remember the indexed columns, its order and many factors that affect the performance. This tool will generate the most optimal queries for all needs.  

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'report_query'
```

And then execute:

    $ bundle install

Or install it yourself as:

    $ gem install report_query

## Usage

This is just an idea till now but this is what I am expecting to do. Lets say we have tables as Account `has_many` Users `has_many` Emails `has_many` EmailConversations `has_many` EmailConversationRecipients. Now task is to find the email conversation of a user where a recipient is `abc@yopmail.com`. 
```ruby
account_id = 123
select_columns = %w[EmailConversations.*]

where_conditions = [{
    'Users.id' => 1,
    'condition_type' => 'column_eq_fixnum'
}, {
    'EmailConversationRecipients.email_address' => 'abc@yopmail.com',
    'condition_type' => 'column_eq_string'
}, {
    'EmailConversationRecipients.email_address' => 'Users.email_address'
    'condition_type' => 'column_eq_column'
}]

page = 1
per_page = 20

ReportQuery.select(select_columns).for_account(account_id).where(where_conditions).page(page).per_page(per_page).generate_query

```
Reading the inputs of select_columns, where_conditions etc, the gem should intelligently understand what tables to use, what joins to use etc. The gem should work the same way as we think.

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/report_query. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [code of conduct](https://github.com/[USERNAME]/report_query/blob/master/CODE_OF_CONDUCT.md).


## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the ReportQuery project's codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/report_query/blob/master/CODE_OF_CONDUCT.md).
