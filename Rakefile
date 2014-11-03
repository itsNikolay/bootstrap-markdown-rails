require 'bundler/gem_tasks'
require 'rubygems'
require 'net/http'

begin
  require 'bundler/setup'
rescue LoadError
  puts 'You must `gem install bundler` and `bundle install` to run rake tasks'
end

require 'bundler'
require 'rake'

desc 'Upload lib files from remote repo'
namespace :source do
  task :download do
    js_filename = 'bootstrap-markdown.js'
    js_url = "https://raw.githubusercontent.com/toopay/bootstrap-markdown/master/js/#{js_filename}"
    js_path = "vendor/assets/javascripts/#{js_filename}"

    css_filename = 'bootstrap-markdown.min.css'
    css_url = "https://raw.githubusercontent.com/toopay/bootstrap-markdown/master/css/#{css_filename}"
    css_path = "vendor/assets/stylesheets/#{css_filename}"

    %w(de fr ja kr nb nl ru sv tr ua zh).each do |locale|
      locale_filename = "bootstrap-markdown.#{locale}.js"
      locale_url = "https://raw.githubusercontent.com/toopay/bootstrap-markdown/master/locale/#{locale_filename}"
      locale_path = "vendor/assets/javascripts/locale/#{locale_filename}"

      response = Net::HTTP.get( URI(locale_url) )
      if File.write(locale_path, response)
        puts %Q{
-->> #{locale_url}
was succesfully uploaded to:
-->> #{locale_path}
}
      end

    end

    response = Net::HTTP.get( URI(js_url) )
    if File.write(js_path, response)
      puts %Q{
-->> #{js_url}
was succesfully uploaded to:
-->> #{js_path}
}
    end

    response = Net::HTTP.get( URI(css_url) )
    if File.write(css_path, response)
      puts %Q{
-->> #{css_url}
was succesfully uploaded to:
-->> #{css_path}
}
    end
  end
end

