
 **1 _ My vpn 1.9** → [Android](https://uplnk.com/f/134a0565/my_vpn_1.9.0.apk) & [link2](https://www.mediafire.com/file/tkjuj75v8gh8s5q/MY+VPN+1.9.0.apk/file)

 **2 _ My vpn 1.9** → [Windows](http://uplnk.com/f/f99ba404/my_vpn.windows.zip)

ابتدا برنامه رو از لینک بالا با فیلتر شکن خاموش دانلود و نصب میکنیم
پس از دانلود و نصب برنامه برنامه رو اجرا میکنیم.

با وارد کردن نام کاربری و رمز عبور خریداری شده وارد برنامه میشویم و با انتخاب یکی از سرور های موجود متصل میشویم.
node {
    // Change `url` value to your own
    git url: 'file:////Users/evildethow/workspace/spike/project-w-property-files.git'

    def inputParams = inputParamsString(new File(pwd()))

    // Change `message` value to the message you want to display
    // Change `description` value to the description you want
    def selectedProperty = input( id: 'userInput', message: 'Choose properties file', parameters: [ [$class: 'ChoiceParameterDefinition', choices: inputParams, description: 'Properties', name: 'prop'] ])

    println "Property: $selectedProperty"

    // Change `job` value to your downstream job name
    // Change `name` value to the name you gave the string parameter in your downstream job
    build job: 'downstream-freestyle', parameters: [[$class: 'StringParameterValue', name: 'prop', value: selectedProperty]]
}

import static groovy.io.FileType.FILES

@NonCPS
def inputParamsString(dir) {
    def list = []

    // If you don't want to search recursively then change `eachFileRecurse` -> `eachFile`
    dir.eachFileRecurse(FILES) {
        // Change `.properties` to the file extension you are interested in
        if(it.name.endsWith('.properties')) {
            // If the full path is required remove `.getName()`
            list << it.getName()
        }
    }

    list.join("\n")
}
