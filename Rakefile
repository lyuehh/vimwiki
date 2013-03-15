require "erubis"
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
  #puts `ls -1 | grep 'md'`
  all_md = Dir.entries('.').select {|d| d.include?('md')}
end

desc 'gen gh-pags'
task :page do
  p = ENV['p']
  raise 'need p, try p=p1 rake page' unless p

  # 1 get all problems
  ps = Dir.entries('.')
    .select{|d| d.include?('md')}
    .map{|d| d.split('.')[0]}
    .select {|d| d != 'README' && d != 'index'}

  # 2 get template
  input = File.read('template/p.html.erb')
  eruby = Erubis::Eruby.new(input)

  p_content = `cat #{p}.md | marked`

  # 5 write html to file
  Dir.chdir('gh-pages/items/');
  File.open("#{p}.html", "w") do |f|
    f.puts eruby.result(binding())
  end
  Dir.chdir('..')
end

desc 'push gh-pages'
task :pushpage do
  Dir.chdir('gh-pages');
  system 'git add .'
  system 'git commit -a -m "update gh-pages"'
  system 'git push origin gh-pages'
  Dir.chdir('..')
  puts 'push gh-pages ok...'
end

desc 're gen pages'
task :allpage do

  # 1 get all problems
  ps = Dir.entries('.')
    .select{|d| d.include?('md')}
    .map{|d| d.split('.')[0]}
    .select {|d| d != 'README' && d != 'index'}

  ps.each do |p|
    system "p=#{p} rake page"
  end
  puts "All page generate done..."
end
