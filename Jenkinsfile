@Library('ZomisJenkins')
import net.zomis.jenkins.Duga
import groovy.json.JsonSlurper

@NonCPS
def perform() {
    def duga = new Duga()
    def url = new URL('https://mods.factorio.com/api/mods?owner=zomis&page_size=100&page=1')
    def data = new JsonSlurper().parseText(url.text)

    println data.results
    def str = new StringBuilder()
    data.results.each {
        def title = it.latest_release.info_json.title
        def latestDownloads = it.latest_release.downloads_count
        def downloads = it.downloads_count
        def message = "$title: $downloads (Latest version: $latestDownloads)"
        println message
        str.append(message)
        str.append('; ')
    }
    duga.dugaResult(str.toString())
}

node {
    stage("Get and report downloads") {
        perform()
    }
}
