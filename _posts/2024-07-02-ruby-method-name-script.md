# Ruby Script: List of Method Names in Files

Today, I began work on a task in which I'll manually check whether several Ruby on Rails controllers and their actions are still used or not.

There are several controller files, so to remain organized, I opted to list up all of the relevant ones. In doing so, I found myself wanting to have a list of their actions (each associated with its controller) as well.

One thing led to another, and I ended up creating this Ruby script that lists up four things:
1. directory
2. controller filename
3. line number on which the action is defined
4. action name (excluding `def`, comments, etc.)

The list is in a simple CSV format for easy transferral into Excel.

<script src="https://gist.github.com/codeconscious/a2afb7225fd387cab84ddacfb4d296fa.js"></script>

Sample output:

```
Directory,Filename,Line,Method
app/controllers,home_controller.rb,2,index
app/controllers,home_controller.rb,4,about_me
```

(There were far more results at work, of course.)

This saved me a lot of time and tedium, and it should make the task far more manageable.
