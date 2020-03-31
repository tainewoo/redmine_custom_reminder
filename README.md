Plugins that allows to create custom email reminders.

**Minimum Rails version - 5.2**


(**$REDMINE_ROOT**) - directory where Redmine is located.

Regular plugin installation:
1) Clone repository to your plugins directory (**$REDMINE_ROOT**)/plugins
2) Create ruby file ```application_job.rb``` in (**$REDMINE_ROOT**)/app/jobs/application_job.rb with following content

    ```ruby
    class ApplicationJob < ActiveJob::Base
      # Automatically retry jobs that encountered a deadlock
      # retry_on ActiveRecord::Deadlocked
    
      # Most jobs are safe to ignore if the underlying records are no longer available
      # discard_on ActiveJob::DeserializationError
    end
    ```

3) In your terminal execute ```bundle install``` at (**$REDMINE_ROOT**) to install needed gems
4) In your terminal execute ```rake redmine:plugins``` at (**$REDMINE_ROOT**) to perform database migration
5) In your terminal execute ```bundle exec whenever -i redmine_custom_reminder -f plugins/redmine_custom_reminder/config/schedule.rb``` at (**$REDMINE_ROOT**)

After last step scheduler will start at 10:00 am every day. You can change it in *(**$REDMINE_ROOT**)plugins/redmine_custom_reminder/config/schedule.rb*. And executing step №5 from instruction.

Update:
For step 5, you can also try to add the CustomReminder command to your cron tasks manually:
/usr/local/bin/bundle exec /usr/local/bin/rails runner -e production "CustomRemindersJob.perform_now"

_Inspired by Redmine Custom Workflows;_
