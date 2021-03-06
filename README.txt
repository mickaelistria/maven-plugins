Personal sandbox for developing maven plugins. Since most of what I do is release engineering of Eclipse plugins/features/p2 sites, most of what you'll find here will be related to continuous integration builds w/ Jenkins/Hudson of Eclipse plugins/features/sites with Tycho (Maven 3).

No warranty provided or implied. Code's free (as in beer) to do w/ as you'd like. 

Licensed under some mix of EPL, WTFPL, and Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported (CC BY-NC-SA 3.0). nickboldt at gmail dot com for more info.

---

Current collection includes:

hudson-boolean-property-toggle-plugin - toggle a boolean field in one or more jobs' config.xml. For example, can enable/disable blocking when upstream jobs are running

hudson-job-publisher-plugin - publish 1 or more new jobs (can override/replace existing jobs, too) via config.xml template file to Hudson/Jenkins server

hudson-job-sync-plugin - pull from Jenkins to a local cache of config.xml files, or push those files back to the server. Very handy for batch-editing a collection of jobs using script (eg., using sed to globally replace strings), then making changes to many jobs at once. Works with view names to restrict which jobs will be affected and regular expressions to filter within a given view, so you can pull/push a handful of jobs or update everything. I use this to maintain the >140 jobs needed to build three streams of JBoss Tools and Developer Studio.

hudson-job-schedule-checker-plugin - output information about a collection of jobs to see how they're queued up (eg., SVN check times)

org.jboss.tools.util.parentPomUpdater - update a number of pom files to point at a new parent group:artifact:version triplet. Run cmdline w/o options for usage details.

site-aggregator-plugin -  Given a list of folders within a base URL, fetch their contents and collect everything into a single published site

unique-GAV-plugin - Check for non-unique GAVs and apply best practices to G:A:V naming

--

Also, there's some in-progress work which is probably not useful to anyone:


sample-maven-plugin

sample-maven-project-depends-on-plugins

--

These were deleted because there are replacements in Tycho 0.14:

tycho-p2-source-feature-plugin - https://repository.jboss.org/nexus/index.html#nexus-search;quick~tycho-source-feature-plugin
	To use this, see http://wiki.eclipse.org/Minerva#Source
	Example:
		http://anonsvn.jboss.org/repos/jbosstools/branches/jbosstools-3.3.x/build/parent/pom.xml
		http://anonsvn.jboss.org/repos/jbosstools/branches/jbosstools-3.3.x/jmx/features/org.jboss.tools.jmx.feature/pom.xml
		http://anonsvn.jboss.org/repos/jbosstools/branches/jbosstools-3.3.x/jmx/site/category.xml

tycho-p2-mirror-plugin - https://repository.jboss.org/nexus/index.html#nexus-search;quick~tycho-p2-extras-plugin
	To use this, see http://wiki.eclipse.org/Tycho/Additional_Tools
	Example:
		http://anonsvn.jboss.org/repos/jbosstools/branches/jbosstools-3.3.x/download.jboss.org/jbosstools/updates/requirements/m2eclipse/pom-juno-1.1.0.20120320-0058.xml

