task default: 'app:setup'
namespace :app do
  desc 'Setup Project'
  task :setup => [:init, :credentials]

  desc 'Setup Gems and Pods'
  task :init do
    sh 'gem', 'install', 'bundler' unless system('which bundle')
    sh 'bundle', 'install', '--binstubs'
    sh 'bundle', 'exec', 'pod', 'install'
  end

  desc 'Set API keys'
  task :credentials do
    tpl_file    = 'NewsPlayer/Credentials~.plist'
    target_file = 'NewsPlayer/Credentials.plist'
    google_api_key = ENV['GOOGLE_API_KEY']
    error "#{tpl_file} does not exist." unless File.exist?(tpl_file)
    error "Specify GOOGLE_API_KEY, like `rake app:credentials GOOGLE_API_KEY=\"AIzaSyB_OrxR6ZYxAr\"`" unless google_api_key
    File.write target_file, File.read(tpl_file).gsub("__YOUR_AUTH_KEY__", google_api_key)
  end

  def error(message = "Something went wrong.")
    STDERR.puts "ERROR: #{message}"
    exit 1
  end

end
