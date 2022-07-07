lane :scanLocalPR do |options|
    xcode_select("/Applications/Xcode.app")
    scan(scheme: "MyProjectNameXcode",
                  force_quit_simulator: true,
                  reset_simulator: true,
                  code_coverage: true,
                  clean: true,
                  destination: "platform=iOS Simulator,name=iPhone 13,OS=15.2",
                  sdk: "iphonesimulator",
                  workspace: "./MyProjectNameXcode.xcworkspace",
                  parallel_testing: false,
                  derived_data_path: "./DerivedData",
                  output_directory: "./sonar-reports",
                  skip_build: true)
    slather(sonarqube_xml: true,
            scheme: "MyProjectNameXcode",
            build_directory: "./DerivedData",
            output_directory: "./sonar-reports",
            workspace: "./MyProjectNameXcode.xcworkspace",
            proj: "./MyProjectNameXcode.xcodeproj",
            ignore: ["Pods/*","SMAPIHelper/*","MyProjectNameXcodeTests/*","Frameworks/*","*View*","*ViewController*","*Analytics*"])
    swiftlint(output_file: "./sonar-reports/swiftlint.txt", ignore_exit_status: true)
    sonar(branch_name: options[:branch_name] ? options[:branch_name] : "unknown")
  end
