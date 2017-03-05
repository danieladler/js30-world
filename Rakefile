require 'rake'
require 'jekyll'

# desc 'Watch sass'
#   task :sasswatch do
#   system 'sass -r sass-globbing --watch sass/style.scss:css/style.css'
# end

desc 'Watch sass files'
task :sasswatch do
  system 'sass -r sass-globbing --watch assets/sass/style.scss:assets/css/style.css'
end

desc 'Watch jekyll files'
task :jekyllwatch do
  system 'bundle exec jekyll serve' # TODO: add --watch
end

desc 'Running Browsersync'
task :browsersync do
  system 'browser-sync start --proxy "localhost:4000" --files "_site/assets/*, _site/*.md, _site/*.html, _site/*.js --no-inject-changes"'
end

def jekyll(opts = '')
  system 'rm -rf _site'
  system 'jekyll ' + opts
end

desc 'Serve'
task :serve do
  threads = []
  %w{jekyllwatch sasswatch browsersync}.each do |task|
    threads << Thread.new(task) do |devtask|
      Rake::Task[devtask].invoke
    end
  end
  threads.each {|thread| thread.join}
  puts threads
end
