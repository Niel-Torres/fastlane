# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

default_platform(:ios)

appScheme = "#{ENV['appScheme']}"

platform :ios do

  desc "Run all lanes"
  lane :scanLocalPR do
    #lint
    #build
    coverage
    sonar

  end

  desc "Build the application"
  lane :build do
    scan(
      scheme: "MyProjectNameXcode",
      workspace: "MyProjectNameXcode.xcworkspace",
      clean: true
    )
  end

  desc "Calculate the code coverage"
  lane :coverage do
    slather(
      scheme: "MyProjectNameXcode",
      workspace: "MyProjectNameXcode.xcworkspace",
      output_directory: "sonar-reports", 
      proj: "MyProjectNameXcode.xcodeproj",
      cobertura_xml: "true"
    )
  end

  desc "Apply swift linting"
  lane :lint do
    swiftlint(
      output_file: "sonar-reports/MyProjectNameXcode-swiftlint.txt",
      ignore_exit_status: true
    )
  end

end
