---
layout: post
title: "Jekyll and rake tasks"
description: ""
category: "general"
tags: [sysadmin,jekyll,rake]
theme_name: dmal
---
{% include JB/setup %}
I decided to try and make some rake tasks to make drafts and publish those drafts.

# Create draft
I have cheated a great deal with this task. I basically copied the post task, and did some minor adjustments to some configs, and off we went.

```rake
desc "Begin a new draft in #{CONFIG['drafts']}"
task :draft do
  abort("rake aborted: '#{CONFIG['drafts']}' directory not found.") unless FileTest.directory?(CONFIG['drafts'])
  title = ENV["title"] || "new-post"
  tags = ENV["tags"] || "[]"
  category = ENV["category"] || ""
  category = "\"#{category.gsub(/-/,' ')}\"" if !category.empty?
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['drafts'], "#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end
    theme_name = CONFIG["theme_name"]
  puts "Creating draft post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts 'description: ""'
    post.puts "category: #{category}"
    post.puts "tags: #{tags}"
    post.puts "theme_name: #{theme_name}"
    post.puts "---"
    post.puts "{% include JB/setup %}"
  end
end # task :draft
```

# Publish task
I wanted to be able to use rake to move files from drafts folder to posts folder, and make sure that the file was named correct. This is a basic task where I either show a list of files to publish, and require the user, aka. me, to issue the same command again, this time with a filename   

```rake
desc "Publish draft"
task :publish do

filename = ENV["filename"] || ""
puts filename
if filename.empty? then
  puts "Please sepcify a filename, like this: rake publish filename=xxx.md"
  puts "This is list a drafts to publish"
  FileList.new(CONFIG['drafts']+'/**') do |d| 
    puts d.pathmap("%f") 
  end
  
else
    date = Time.now.strftime('%Y-%m-%d')
    postfilename = File.join(CONFIG['posts'], "#{date}-#{filename}")
    draftsfilename = File.join(CONFIG['drafts'], "#{filename}")
    puts "Publishing #{filename}"
    FileUtils.mv draftsfilename, postfilename 
    
end 
```
I am sure the publish task can be done in another way, but I think this is a KISS solution, given that I am not, in anyway, used to program in ruby. 