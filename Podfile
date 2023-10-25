use_frameworks!

def tests
    pod 'SwiftyMocky', :path => './'
end

target 'Mocky_Example_iOS' do
    platform :ios, '13.0'
    target 'Mocky_Tests_iOS' do
        inherit! :search_paths
        tests
    end
end

target 'Mocky_Example_iOS_15' do
    platform :ios, '15.0'
    target 'Mocky_Tests_iOS_15' do
        inherit! :search_paths
        tests
    end
end

target 'Mocky_Example_tvOS' do
    platform :tvos, '9.0'
    target 'Mocky_Tests_tvOS' do
        inherit! :search_paths
        tests
    end
end

target 'Mocky_Example_macOS' do
    platform :macos, '10.13'
    target 'Mocky_Tests_macOS' do
        inherit! :search_paths
        tests
    end
end

post_install do |pi|
  fix_toolchain_dir(pi)
end

def fix_toolchain_dir(pod_installer)
  pod_installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        if config.base_configuration_reference
          xcconfig_path = config.base_configuration_reference.real_path
          xcconfig = File.read(xcconfig_path)
          xcconfig_mod = xcconfig.gsub(/DT_TOOLCHAIN_DIR/, "TOOLCHAIN_DIR")
          File.open(xcconfig_path, "w") { |file| file << xcconfig_mod }
        end
      end
    end
end
