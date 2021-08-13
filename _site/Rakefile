require 'fileutils'

def timestamp_filename(file)
  dir  = File.dirname(file)
  base = File.basename(file, ".*")
  time = Time.now.to_i  # or format however you like
  ext  = File.extname(file)
  File.join(dir, "#{time}_#{base}#{ext}")
end

namespace :draft do
  desc "Creating a new draft for a post file"
  task :new do
    puts "What's the name for your draft?"
    @name = STDIN.gets.chomp
    @slug = "#{@name}"
    @slug = @slug.tr('ÁáÉéÍíÓóÚú', 'AaEeIiOoUu')
    @slug = @slug.downcase.strip.gsub(' ', '-')
    @slug = timestamp_filename(@slug)
    FileUtils.touch("_drafts/#{@slug}.md")
    open("_drafts/#{@slug}.md", 'a' ) do |file|
      file.puts "---"
      file.puts "layout: post"
      file.puts "title: #{@name}"
      file.puts "description: maximum 155 char description"
      file.puts "category: blog"
      file.puts "tag: blog"
      file.puts "---"
    end
    puts "Created #{@slug}"
  end


namespace :candidate do
  desc "Creating a new candidate for release file"
  task :new do
    puts "What's the name for your candidate?"
    @name = STDIN.gets.chomp
    @slug = "#{@name}"
    @slug = @slug.tr('ÁáÉéÍíÓóÚú', 'AaEeIiOoUu')
    @slug = @slug.downcase.strip.gsub(' ', '-')
    @slug = timestamp_filename(@slug)
    FileUtils.touch("_drafts/#{@slug}.md")
    open("_drafts/#{@slug}.md", 'a' ) do |file|
      file.puts "---"
      file.puts "layout: post"
      file.puts "title: #{@name}"
      file.puts "description: maximum 155 char description"
      file.puts "category: blog"
      file.puts "tag: blog"
      file.puts "---"
    end
    puts "Created #{@slug}"
  end

  desc "copy draft to production post!"
  task :ready do
    puts "Posts in _drafts:"
    Dir.foreach("_drafts") do |fname|
      next if fname == '.' or fname == '..' or fname == '.keep'
      puts fname
    end
    puts "what's the name of the draft to post?"
    @post_name = STDIN.gets.chomp
    @post_date = Time.now.strftime("%F")
    FileUtils.mv("_drafts/#{@post_name}", "_posts/#{@post_name}")
    FileUtils.mv("_posts/#{@post_name}", "_posts/#{@post_date}-#{@post_name}")
    puts "Post copied and ready to deploy!"
  end
end