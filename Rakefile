task :default do
  Rake::Tasks['help'].invoke
end

desc 'help'
task :help do
  puts 'rake help : show this help'
  puts 'rake push : push to github'
  puts 'file=vim rake preview : preview vim.md in browser'
  puts 'rake deploy : convert md to html, and push html to github'
end

desc 'push'
task :push do
  sh 'git push origin master'
end

desc 'preview a md file'
task 'preview' do
  file = ENV['file']
  if !File.exists?(file + '.md') 
    raise "no #{file}.md found in current dir"
  end
  if `which marked` === ""
    raise "marked is not installed, npm install marked -g"
  end
  `marked -i #{file}.md -o /tmp/#{file}.html`
  `open /tmp/#{file}.html`
end

desc 'deploy md file to github'
task :deploy do

end


