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
    #coverage
    #sonar
    sonarLocalPR
  end

  desc "Run sonar Local PR"
  lane :sonarLocalPR do
    xcode_select("/Applications/Xcode.app")
    scan(
      scheme: "MyProjectName", 
      force_quit_simulator: true, 
      reset_simulator: true, 
      code_coverage: true, 
      clean: true, 
      destination: "platform=iOS Simulator,name=iPhone 13", 
      sdk: "iphonesimulator",
      workspace: "./MyProjectName.xcworkspace", 
      parallel_testing: false,
      derived_data_path: "./DerivedData", 
      output_directory: "./reports", 
      skip_build: true,
      fail_build: false)
    slather(
      sonarqube_xml: true, 
      scheme: "MyProjectName", 
      build_directory: "./DerivedData", 
      output_directory: "./reports", 
      workspace: "./MyProjectName.xcworkspace", 
      proj: "./MyProjectName.xcodeproj", 
      ignore: ["Pods/**","SMAPIHelper/**","Frameworks/**","**/*View*","**/*ViewController*","**/*Analytics*","**/Analytics/*","MyProjectName/Business/Resources/**.html","MyProjectName/Localization/**.html"])
    #lizard(source_folder: "[SOURCE_FOLDER]", language: "swift", export_type: "xml", report_file: "reports/lizard-report.xml")
    #swiftlint(output_file: "./reports/swiftlint.txt", ignore_exit_status: true)
    sonar
  end


  desc "Build the application"
  lane :build do
    scan(
      scheme: "MyProjectName",
      workspace: "MyProjectName.xcworkspace",
      clean: true,
      fail_build: false
    )
  end

  desc "Calculate the code coverage"
  lane :coverage do
    slather(
      scheme: "MyProjectName",
      workspace: "MyProjectName.xcworkspace",
      output_directory: "sonar-reports", 
      proj: "MyProjectName.xcodeproj",
      cobertura_xml: "true"
    )
  end

  desc "Apply swift linting"
  lane :lint do
    swiftlint(
      output_file: "sonar-reports/MyProjectName-swiftlint.txt",
      ignore_exit_status: true
    )
  end

end
