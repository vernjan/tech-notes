# Jenkins

## List all jobs without view
- to keep things organized
- run in script console
    ```groovy
    def allJobs = Jenkins.instance.getView('all').items.collect {
        it.fullDisplayName
    }
    
    
    def jobsInViews = Jenkins.instance.views
        .findAll { view -> view.name != "all" }
        .collect { view ->
            view.items.collect {
                it.fullDisplayName
            }
        }.flatten()
    
    
    (allJobs - jobsInViews).each { println it }
    ```