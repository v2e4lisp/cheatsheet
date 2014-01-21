# ruby/rails

## ensure only one process for some rake task
FROM [stack overflow](http://stackoverflow.com/questions/3983883/how-to-ensure-a-rake-task-only-running-a-process-at-a-time)

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

similar for [shell script](http://stackoverflow.com/questions/185451/quick-and-dirty-way-to-ensure-only-one-instance-of-a-shell-script-is-running-at)



