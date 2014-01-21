# ruby/rails

## ensure only one process for some rake task
```ruby
task :my_task do
  pid_file = '/tmp/my_task.pid'
  raise 'pid file exists!' if File.exists? pid_file
  File.open(pid_file, 'w') <<  Process.pid
  begin
    run_task
  ensure
    File.delete pid_file
  end
end
```



