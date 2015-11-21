CWD=File.expand_path(File.dirname(__FILE__))

desc "Handling initial setup and linking"
task :init do
  puts "pulling submodules"
  system "cd #{CWD} && git submodule update --init"
  replace_files
  setperms
end

desc "Update dotfiles to most recent version"
task :update do
  puts "pulling latest from repo"
  system "cd #{CWD} && git pull origin master"
  system "cd #{CWD} && git submodule foreach git pull origin master"
  replace_files
  setperms
end

desc "Set permissions - take away perms from group and other"
task :setperms do
  setperms
end

def replace_files
  files = [ '.bashrc',
            '.bash_profile',
            '.vim',
            '.vimrc',
            '.gvimrc',
  ]
  files.each do |file|
    system "rm -rf #{ENV['HOME']}/#{file}"
  end

  link_file("#{CWD}/bash/_bashrc", "#{ENV['HOME']}/.bashrc")
  link_file("#{CWD}/bash/_bash_profile", "#{ENV['HOME']}/.bash_profile")
  link_file("#{CWD}/vim/_vimrc", "#{ENV['HOME']}/.vimrc")
  link_file("#{CWD}/vim/_gvimrc", "#{ENV['HOME']}/.gvimrc")
  link_file("#{CWD}/vim", "#{ENV['HOME']}/.vim")
  link_file("#{CWD}/_config/awesome", "#{ENV['HOME']}/.config/awesome")
end

def link_file(src, target)
  system "ln -fs #{src} #{target}"
end

def setperms
  system "chmod -R g-rwx,o-rwx #{CWD}"
end
