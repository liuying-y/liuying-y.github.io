require 'rake'

task :build do
  sh "bundle exec jekyll build"
  sh "rm -rf docs"
  sh "mv _site docs"
end

task :serve do
  sh "bundle exec jekyll serve"
end

task :clean do
  sh "bundle exec jekyll clean"
end