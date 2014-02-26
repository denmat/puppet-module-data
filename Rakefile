require 'rake'
  @puppet_file = File.expand_path(File.join(__FILE__, '..', 'lib/puppet/indirector/data_binding/hiera.rb')) 
  @hiera_file = File.expand_path(File.join(__FILE__, '..', 'lib/hiera/backend/module_data_backend.rb'))

  # kinda should work 
  def rh_puppet_path
    rh_puppet_path = %x[find /usr/lib/ruby -type d -name 'puppet' | head -n 1]
  end

  def rh_hiera_path
    hiera_path = %x[find /usr/lib/ruby -type d -name 'hiera' | head -n 1]
  end

  def hiera_helper_gem
    if %x[gem list |grep hiera-puppet-helper] 
      hiera_helper = %x[find /usr/lib/ruby -type d -name 'hiera-puppet-helper*' |head -n 1]
    else
      nil
    end
  end

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

  desc 'deploy to RH family'
  task :install_into_rh  do 
    sh %{cp #{@puppet_file} #{rh_puppet_path}/indirector/data_binding/} do |ok, res|
      raise "failed to install into #{rh_puppet_path}/indirector/data_binding/" unless ok
    end
    sh %{cp #{@hiera_file} #{hiera_path}/backend/} do |ok, res|
      raise "failed to install into #{hiera_path}/backend" unless ok
    end
    if hiera_helper_gem 
      sh %{cp #{@hiera_file} #{hiera_helper_gem}/lib/hiera/backend/} do |ok, res|
        raise "failed to install module_data_backend.rb into hiera-puppet-helper gem" unless ok
      end
    end
  end

