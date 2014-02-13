require 'rake'

  @puppet_file = File.expand_path(File.join(__FILE__), 'lib/puppet/indirector/data_binding/hiera.rb') 
  @hiera_file = File.expand_path(File.join(__FILE__), 'lib/hiera/backend/module_data_backend.rb')

  desc 'install into the local gemsets' 
  task :install_into_gemset, :gemset, :puppet_version, :hiera_version, :hiera_puppet_helper_version do |t,args|
    sh %{cp #{@puppet_file} ~/.rvm/gems/#{args[:gemset]}/gems/#{args[:puppet_version]}/lib/puppet/indirector/data_binding/} do |ok, res|
      puts "installed lib/puppet/indirector/data_binding/hiera.rb" if ok
    end
    sh %{cp #{@hiera_file} ~/.rvm/gems/#{args[:gemset]}/gems/#{args[:hiera_version]}/lib/hiera/backend/module_data_backend.rb} do |ok, res|
      puts "installed lib/hiera/backend/module_data_backend.rb" if ok
    end
    sh %{cp #{@hiera_file} ~/.rvm/gems/#{args[:gemset]}/gems/#{args[:hiera_puppet_helper_version]}/lib/hiera/backend/module_data_backend.rb} do |ok, res|
      puts "installed lib/hiera/backend/module_data_backend.rb" if ok
    end
  end
