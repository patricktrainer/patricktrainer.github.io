
---
    title: Google-Site-Reliability-Engineering
    date: 2021-01-01    
    draft: true
    tags: []
---
# Google-Site-Reliability-EngineeringData pipelines go as far back as co-routines [[Con63]](https://landing.google.com/sre/sre-book/chapters/bibliography), the DTSS communication files [[Bul80]](https://landing.google.com/sre/sre-book/chapters/bibliography), the UNIX pipe [[McI86]](https://landing.google.com/sre/sre-book/chapters/bibliography), and later, ETL pipelines,[116](https://landing.google.com/sre/sre-book/chapters/data-processing-pipelines/) but such pipelines have gained increased attention with the rise of "Big Data," or "datasets that are so large and so complex that traditional data processing applications are inadequate.
"[117](https://landing.google.com/sre/sre-book/chapters/data-processing-pipelines/)
# Initial Effect of Big Data on the Simple Pipeline Pattern
Programs that perform periodic or continuous transformations on Big Data are usually referred to as "simple, one-phase pipelines."
# Drawbacks of Periodic Pipelines in Distributed Environments
Big Data periodic pipelines are widely used at Google, and so Google’s cluster management solution includes an alternative scheduling mechanism for such pipelines.
Moiré load pattern in shared infrastructure
When an inherently one-shot batch pipeline is overwhelmed by business demands for continuously updated results, the pipeline development team usually considers either refactoring the original design to satisfy current demands, or moving to a continuous pipeline model.
Although all pipeline data may be stored in the Task Master, the best performance is usually achieved when only pointers to work are stored in the Task Master, and the actual input and output data is stored in a common filesystem or other storage.
The model-view-controller design pattern as adapted for Google Workflow
We can increase pipeline depth to any level inside Workflow by subdividing processing into task groups held in the Task Master.
Because all pipeline configuration in Workflow is stored inside the Task Master in the same form as the work units themselves, in order to commit work, a worker must own an active lease *and* reference the task ID number of the configuration it used to produce its result.
