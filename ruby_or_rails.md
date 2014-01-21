# ruby/rails

## ensure only one process for some rake task

```ruby
task :my_task do
  pid_file = '/tmp/my_task.pid'
  raise 'pid file exists!' if File.exists? pid_file
  File.open(pid_file, 'w') << {|f| f.puts Process.pid }
  begin
    run_task
  ensure
    File.delete pid_file
  end
end
```
[detail on stack overflow](http://stackoverflow.com/questions/3983883/how-to-ensure-a-rake-task-only-running-a-process-at-a-time)

OR

```ruby
File.new("/tmp/task.lock").flock( File::LOCK_NB | File::LOCK_EX )
```
[detail on stack overflow](http://stackoverflow.com/questions/661684/how-do-i-ensure-only-one-instance-of-a-ruby-script-is-running-at-a-time)



