require 'rake'
  @puppet_file = File.expand_path(File.join(__FILE__, '..', 'lib/puppet/indirector/data_binding/hiera.rb')) 
  @hiera_file = File.expand_path(File.join(__FILE__, '..', 'lib/hiera/backend/module_data_backend.rb'))

  # kinda should work 
  def rh_puppet_path
    rh_puppet_path = %x[find /usr/lib/ruby -type d -name 'puppet' |grep -v puppetx | head -n 1].chomp
  end

  def rh_hiera_path
    hiera_path = %x[find /usr/lib/ruby -type d -name 'hiera' | head -n 1].chomp
  end

  def hiera_helper_gem
    if %x[gem list |grep hiera-puppet-helper] 
      %x[find /usr/lib/ruby -type d -name 'hiera-puppet-helper*' |head -n 1].chomp
      gemset = which_gemset
      if gemset != ''
        %x[find ~/.rvm/gems/#{gemset} -type d -name 'hiera-puppet-helper*' |head -n 1].chomp
      end
    else
      return nil
    end
  end

  def which_gemset
    %x[rvm current].chomp
  end

  def which_puppet
    %x[puppet --version].chomp
  end

  def which_hiera
    %x[hiera --version].chomp
  end

  desc 'install into the local gemsets' 
  task :install_into_gemset  do 

    gemset = which_gemset
    puppet_version = which_puppet
    hiera_version = which_hiera

    sh %{cp #{@puppet_file} ~/.rvm/gems/#{gemset}/gems/puppet-#{puppet_version}/lib/puppet/indirector/data_binding/} do |ok, res|
      puts "installed lib/puppet/indirector/data_binding/hiera.rb" if ok
    end
    sh %{cp #{@hiera_file} ~/.rvm/gems/#{gemset}/gems/#{hiera_version}/lib/hiera/backend/module_data_backend.rb} do |ok, res|
      puts "installed lib/hiera/backend/module_data_backend.rb" if ok
    end
    if hiera_helper_gem != ''
      sh %{cp #{@hiera_file} ~/.rvm/gems/#{gemset}/gems/#{hiera_puppet_helper_version}/lib/hiera/backend/module_data_backend.rb} do |ok, res|
        puts "installed lib/hiera/backend/module_data_backend.rb" if ok
      end
    end
  end

  desc 'deploy to RH family'
  task :install_into_rh  do 

    @rh_puppet_path = rh_puppet_path
    @hiera_path = rh_hiera_path
    @hiera_helper_gem = hiera_helper_gem

    sh %{cp #{@puppet_file} #{@rh_puppet_path}/indirector/data_binding/} do |ok, res|
      raise "failed to install into #{@rh_puppet_path}/indirector/data_binding/" unless ok
    end
    sh %{cp #{@hiera_file} #{@hiera_path}/backend/} do |ok, res|
      raise "failed to install into #{@hiera_path}/backend" unless ok
    end
    if @hiera_helper_gem != ''
      sh %{cp #{@hiera_file} #{@hiera_helper_gem}/lib/hiera/backend/} do |ok, res|
        raise "failed to install module_data_backend.rb into hiera-puppet-helper gem" unless ok
      end
    end
  end

