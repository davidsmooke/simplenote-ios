source 'https://cdn.cocoapods.org/'

unless ['BUNDLE_BIN_PATH', 'BUNDLE_GEMFILE'].any? { |k| ENV.key?(k) }
  raise 'Please run CocoaPods via `bundle exec`'
end

inhibit_all_warnings!
use_frameworks!

platform :ios, '13.0'
workspace 'Simplenote.xcworkspace'

# Main
#
abstract_target 'Automattic' do

  # Main Target
  #
  target 'Simplenote' do
    # Third Party
    #
    pod 'Gridicons', '~> 0.18'
    pod 'AppCenter', '~> 4.4.3'
    pod 'AppCenter/Distribute', '~> 4.4.3'

    # Automattic
    #
    pod 'Automattic-Tracks-iOS', '~> 0.13'
    #		pod 'Automattic-Tracks-iOS', :git => 'https://github.com/Automattic/Automattic-Tracks-iOS.git', :branch => 'add/support-for-tracking-crashes'
    pod 'Simperium', '1.9.0'
    pod 'WordPress-Ratings-iOS', '0.0.2'

    # Testing Target
    #
    target 'SimplenoteTests' do
      inherit! :search_paths
    end
  end

  # Extension Target
  #
  target 'SimplenoteShare' do
    # Third Party
    #
    pod 'ZIPFoundation', '~> 0.9.9'
  end
end


# Post Install
#
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      # Remove min deploy target to clean up build warnings.
      # See: https://stackoverflow.com/a/64048124
      config.build_settings.delete 'IPHONEOS_DEPLOYMENT_TARGET'
      # Fix a code signing issue in Xcode 14 beta.
      # This solution is suggested here: https://github.com/CocoaPods/CocoaPods/issues/11402#issuecomment-1189861270
      config.build_settings['CODE_SIGN_IDENTITY'] = ''
    end
  end
end
