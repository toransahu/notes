multi/poly-repo

differentiator:

pros:

cons:
- autonomy is provided by isolation, and isolation harms collaboration
monolith

(multi-project/app) monorepo (monolithic repository)
initial idea:
-     You want a single source of truth.
    You want to share and reuse code easily.
    You want visibility to manage dependencies (e.g., If you make a change, what else will be impacted?).
    You want to make atomic changes (e.g., one operation to make a change across multiple projects).
    You want teams to collaborate more.
    You want to make large-scale changes (e.g., code refactoring).
differentiator:
	- need manual tooling or have to use available monorepo helper tools liek bazel, nx, lerna, bilt etc
	- each package is independently packaged, and so if we change just one package, we can build only that package (and its dependents)
	- if we change just one package, we need to run the tests only for that package (and its dependents).
	- ?? shall this enfore that - CI should test the dependents by installing current version of shared-lib packages?
	- ?? For instance, you can make atomic changes (one action to make a change across multiple projects). [only makes sense if we do above]

true definition:
- it is really about reusable code sharing (code,utils,tooling,standards) & project/app seperation,buil,test,release,deployment
[!monorepo-dir](https://res.cloudinary.com/practicaldev/image/fetch/s--R_IYSI05--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1bdwiyhgbvetfiezvg7u.png)
- if not monorepo then you're not doing continuous integration - but frequent integration (as you'll do in polyrepo using dependency injection)


monorepo vs monolith


Ref:

1. https://monorepo.tools/
1. https://blog.nrwl.io/misconceptions-about-monorepos-monorepo-monolith-df1250d4b03c
1. https://medium.com/@magenta2127/monorepo-vs-multi-repo-vs-monolith-7c4a5f476009
1. https://www.linkedin.com/pulse/monolithic-repository-vs-monorepo-oleg-dulin/
1. https://www.perforce.com/blog/vcs/what-monorepo
1. https://github.com/giltayar/bilt/blob/main/docs/monolithic-vs-monorepos.md
1. https://www.reddit.com/r/learnprogramming/comments/1b9rm6m/monorepo_multirepo_vs_monolith_microservice/
1. https://dev.to/elliotalexander/monorepos-best-practice-for-scaling-a-jam-stack-dl
1. https://www.linkedin.com/pulse/mastering-react-monorepos-effortless-code-sharing-mirza-hassan/
1. https://docs.devland.is/technical-overview/monorepo
1. https://medium.com/@vitorbritto/building-a-monorepo-the-right-way-f8bea3138681
1. https://christianlydemann.com/a-guide-to-sharing-code-between-projects/
1. https://thekarel.gitbook.io/best-practices/constraints/monorepo
1. https://www.linkedin.com/pulse/demystifying-monorepo-streamlining-software-ziran-fuzooly-0g4bc/
1. https://blog.bitsrc.io/5-mistakes-that-you-should-avoid-with-a-monorepo-956e8fe3633e
1. https://qeunit.com/blog/how-google-does-monorepo/
1. https://medium.com/@Jakeherringbone/you-too-can-love-the-monorepo-d95d1d6fcebe (good read)
1. https://cacm.acm.org/research/why-google-stores-billions-of-lines-of-code-in-a-single-repository/ (about google)
	- In contrast, with a monolithic source tree it makes sense, and is easier, for the person updating a library to update all affected dependencies at the same time. The technical debt incurred by dependent systems is paid down immediately as changes are made. 
1. https://en.wikipedia.org/wiki/Monorepo
1. https://dev.to/amburi/monolithic-microservices-and-mono-repo-architecture-4o33
1. https://alessandroraffa.medium.com/the-evolution-of-software-repositories-monoliths-monorepos-and-multi-repos-44c63ba83697
1. https://news.ycombinator.com/item?id=33585104
1. https://www.benlorantfy.com/the-problem-with-shared-libraries-and-monorepos
1. https://polylith.gitbook.io/polylith
