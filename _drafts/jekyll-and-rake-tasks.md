---
layout: post
title: "Jekyll and rake tasks"
description: ""
category: "general"
tags: [sysadmin,jekyll,rake]
theme_name: dmal
---
{% include JB/setup %}
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



desc "Publish draft"
task :publish do

filename = ENV["filename"] || ""
puts filename
if filename.empty? then
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