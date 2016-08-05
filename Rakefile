desc "Create a new post with the command 'rake new_post['post title here']'"
task :new_post, [:post_name, :image_dir] do |t, args|
  time = Time.now
  date = time.strftime('%Y-%m-%d')
  slug = args.post_name.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '') #slug the title, to make a filemanmt

  file = File.open("_posts/#{date}-#{slug}.markdown", "w")
  file.puts <<-eom
---
layout: post
title: #{args.post_name}
date: #{time.strftime('%Y-%m-%d %H:%M:%S %z')}
---

eom
  file.close
end
