---
layout: post
title: Maven Madness
---

{{ page.title }}
================

<p class="meta">5 December 2010 - Bolinas</p>

The clojure community seems to have adopted maven as the way to manage
dependency fetching for clojure projects. I suppose this makes sense
to folks coming from a Java background but, to me, it seems
lunacy. I'm always somewhat suspect of automagic
installation/dependency-management tools (although xach's
[quicklisp](http://www.quicklisp.org) is pretty nice). Maven always
bothers me because it downloads and installs a ton of things of which
I have never heard. The latest example is what happens when one tries
to build the latest clojure-contrib.

I suppose, before getting into the details of the maven madness I see,
I should addresss the issue of why I'm building clojure-contrib at
all. Another difference between, say, the SBCL community and the
clojure community is that the SBCL folks generally take the attitude
of "here's the source and a binary that you can use to bootstrap
building your own compiler; now go off and have fun." In the clojure
community it seems to be more "here's where you can download the jars
you need -- and building things like clojure itself and
clojure-contrib is best left to the experts." It's not that that's
necessarily a bad thing, but it's certainly not what I'm used to. So,
my first instinct is to biuld clojure, then build clojure-contrib,
then try to get my stuff working on it. I suppose I should also say
that the motivation for this is that I want to get my clojure projects
like [shortcut](https://github.com/slyrus/shortcut) and
[chemiclj](https://github.com/slyrus/chemiclj) ready for clojure 1.3.

Ok, now onto the details. First, I fetch and build the latest clojure. No problem there. Now, I'll use that jar to build a new clojure-contrib:


    (sly@barbaresco):~/src/clojure/clojure-contrib$ mvn package -Dclojure.jar=/Users/sly/src/clojure/clojure/clojure-1.3.0-alpha3-SNAPSHOT.jar 
    [INFO] Scanning for projects...
    [INFO] Reactor build order: 
    [INFO]   Clojure Contrib parent module
    [INFO]   Unnamed - org.clojure.contrib:def:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:types:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:generic:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:accumulators:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:agent-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:base64:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:jar:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:classpath:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:combinatorics:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:command-line:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:complex-numbers:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:cond:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:seq:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:condition:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:core:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:graph:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:except:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:dataflow:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:datalog:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:error-kit:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:fcase:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:find-namespaces:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:fnmap:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:prxml:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:gen-html-docs:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:greatest-least:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:import-static:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:java-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:jmx:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:json:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:lazy-seqs:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:lazy-xml:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:logging:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:macro-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:macros:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:map-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:math:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:miglayout:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:mmap:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:ns-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:mock:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:monads:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:monadic-io-streams:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:priority-map:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:stream-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:probabilities:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:profile:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:reflect:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:repl-ln:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:repl-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:server-socket:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:set:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:singleton:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:sql:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:with-ns:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:strint:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:swing-utils:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:trace:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:zip-filter:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:complete:jar:1.3.0-SNAPSHOT
    [INFO]   Unnamed - org.clojure.contrib:standalone:jar:1.3.0-SNAPSHOT
    [INFO]   Clojure Contrib
    [INFO] ------------------------------------------------------------------------
    [INFO] Building Clojure Contrib parent module
    [INFO]    task-segment: [package]
    [INFO] ------------------------------------------------------------------------
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/plugins/maven-site-plugin/2.0-beta-7/maven-site-plugin-2.0-beta-7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/plugins/maven-plugins/11/maven-plugins-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-parent/8/maven-parent-8.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/plugins/maven-site-plugin/2.0-beta-7/maven-site-plugin-2.0-beta-7.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven/2.0.9/maven-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.5.8/plexus-utils-1.5.8.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus/2.0.2/plexus-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/junit/junit/3.8.2/junit-3.8.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-webdav/1.0-beta-2/wagon-webdav-1.0-beta-2.pom

    Downloading: http://repo1.maven.org/maven2/slide/slide-webdavlib/2.1/slide-webdavlib-2.1.pom

    Downloading: http://repo1.maven.org/maven2/commons-httpclient/commons-httpclient/2.0.2/commons-httpclient-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/commons-logging/commons-logging/1.0.3/commons-logging-1.0.3.pom

    Downloading: http://repo1.maven.org/maven2/jdom/jdom/1.0/jdom-1.0.pom

    Downloading: http://repo1.maven.org/maven2/de/zeigermann/xml/xml-im-exporter/1.1/xml-im-exporter-1.1.pom

    Downloading: http://repo1.maven.org/maven2/commons-logging/commons-logging/1.0.4/commons-logging-1.0.4.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.9/maven-reporting-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.0-alpha-10/doxia-sink-api-1.0-alpha-10.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia/1.0-alpha-10/doxia-1.0-alpha-10.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-parent/6/maven-parent-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.pom

    Downloading: http://repo1.maven.org/maven2/commons-lang/commons-lang/2.3/commons-lang-2.3.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/enforcer/enforcer-api/1.0-beta-1/enforcer-api-1.0-beta-1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/enforcer/enforcer-rules/1.0-beta-1/enforcer-rules-1.0-beta-1.pom

    Downloading: http://repo1.maven.org/maven2/org/beanshell/bsh/2.0b4/bsh-2.0b4.pom

    Downloading: http://repo1.maven.org/maven2/org/beanshell/beanshell/2.0b4/beanshell-2.0b4.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.5.8/plexus-utils-1.5.8.jar
    Downloading: http://repo1.maven.org/maven2/commons-lang/commons-lang/2.3/commons-lang-2.3.jar
    Downloading: http://repo1.maven.org/maven2/org/beanshell/bsh/2.0b4/bsh-2.0b4.jar
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/enforcer/enforcer-api/1.0-beta-1/enforcer-api-1.0-beta-1.jar



    Downloading: http://repo1.maven.org/maven2/org/apache/maven/enforcer/enforcer-rules/1.0-beta-1/enforcer-rules-1.0-beta-1.jar


    [INFO] [enforcer:enforce {execution: enforce-maven}]
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-model/2.0.2/maven-model-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-project/2.0.2/maven-project-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-profile/2.0.2/maven-profile-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-repository-metadata/2.0.2/maven-repository-metadata-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-core/2.0.2/maven-core-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-settings/2.0.2/maven-settings-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-file/1.0-alpha-6/wagon-file-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-providers/1.0-alpha-6/wagon-providers-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.2/maven-plugin-parameter-documenter-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-http-lightweight/1.0-alpha-6/wagon-http-lightweight-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.2/maven-reporting-api-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.2/maven-reporting-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.2/maven-error-diagnostics-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-registry/2.0.2/maven-plugin-registry-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-ssh-external/1.0-alpha-6/wagon-ssh-external-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.2/maven-plugin-descriptor-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-monitor/2.0.2/maven-monitor-2.0.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-ssh/1.0-alpha-6/wagon-ssh-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/com/jcraft/jsch/0.1.24/jsch-0.1.24.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-api/2.0.2/maven-plugin-api-2.0.2.pom

    [INFO] [build-helper:add-source {execution: add-clj-source}]
    [INFO] Source directory: /Users/sly/src/clojure/clojure-contrib/modules/parent/src/main/clojure added.
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven/2.2.1/maven-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-exec/1.0.1/commons-exec-1.0.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-parent/11/commons-parent-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-io/1.3.2/commons-io-1.3.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-parent/3/commons-parent-3.pom

    Downloading: http://repo1.maven.org/maven2/commons-lang/commons-lang/2.5/commons-lang-2.5.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-parent/12/commons-parent-12.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-toolchain/2.2.1/maven-toolchain-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-core/2.2.1/maven-core-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-settings/2.2.1/maven-settings-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-model/2.2.1/maven-model-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.5.15/plexus-utils-1.5.15.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-interpolation/1.11/plexus-interpolation-1.11.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-components/1.1.14/plexus-components-1.1.14.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-file/1.0-beta-6/wagon-file-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-providers/1.0-beta-6/wagon-providers-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon/1.0-beta-6/wagon-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-provider-api/1.0-beta-6/wagon-provider-api-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.4.2/plexus-utils-1.4.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.2.1/maven-plugin-parameter-documenter-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-http-lightweight/1.0-beta-6/wagon-http-lightweight-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-http-shared/1.0-beta-6/wagon-http-shared-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/nekohtml/xercesMinimal/1.9.6.2/xercesMinimal-1.9.6.2.pom

    Downloading: http://repo1.maven.org/maven2/nekohtml/nekohtml/1.9.6.2/nekohtml-1.9.6.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-http/1.0-beta-6/wagon-http-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-webdav-jackrabbit/1.0-beta-6/wagon-webdav-jackrabbit-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/jackrabbit/jackrabbit-webdav/1.5.0/jackrabbit-webdav-1.5.0.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/jackrabbit/jackrabbit-parent/1.5.0/jackrabbit-parent-1.5.0.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/jackrabbit/jackrabbit-jcr-commons/1.5.0/jackrabbit-jcr-commons-1.5.0.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.5.3/slf4j-api-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/slf4j-parent/1.5.3/slf4j-parent-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/commons-httpclient/commons-httpclient/3.0/commons-httpclient-3.0.pom

    Downloading: http://repo1.maven.org/maven2/commons-codec/commons-codec/1.2/commons-codec-1.2.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/slf4j-nop/1.5.3/slf4j-nop-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/slf4j-jdk14/1.5.6/slf4j-jdk14-1.5.6.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/slf4j-parent/1.5.6/slf4j-parent-1.5.6.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.5.6/slf4j-api-1.5.6.pom

    Downloading: http://repo1.maven.org/maven2/org/slf4j/jcl-over-slf4j/1.5.6/jcl-over-slf4j-1.5.6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.2.1/maven-reporting-api-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting/2.2.1/maven-reporting-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.1/doxia-sink-api-1.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia/1.1/doxia-1.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-logging-api/1.1/doxia-logging-api-1.1.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-30/plexus-container-default-1.0-alpha-30.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-containers/1.0-alpha-30/plexus-containers-1.0-alpha-30.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-profile/2.2.1/maven-profile-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-artifact/2.2.1/maven-artifact-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-repository-metadata/2.2.1/maven-repository-metadata-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-error-diagnostics/2.2.1/maven-error-diagnostics-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-project/2.2.1/maven-project-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-artifact-manager/2.2.1/maven-artifact-manager-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/backport-util-concurrent/backport-util-concurrent/3.1/backport-util-concurrent-3.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-registry/2.2.1/maven-plugin-registry-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/commons-cli/commons-cli/1.2/commons-cli-1.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-ssh-external/1.0-beta-6/wagon-ssh-external-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-ssh-common/1.0-beta-6/wagon-ssh-common-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-6/plexus-interactivity-api-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-interactivity/1.0-alpha-6/plexus-interactivity-1.0-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-components/1.1.9/plexus-components-1.1.9.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus/1.0.10/plexus-1.0.10.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.4/plexus-utils-1.4.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus/1.0.9/plexus-1.0.9.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-descriptor/2.2.1/maven-plugin-descriptor-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-monitor/2.2.1/maven-monitor-2.2.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/wagon/wagon-ssh/1.0-beta-6/wagon-ssh-1.0-beta-6.pom

    Downloading: http://repo1.maven.org/maven2/com/jcraft/jsch/0.1.38/jsch-0.1.38.pom

    Downloading: http://repo1.maven.org/maven2/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.pom

    Downloading: http://repo1.maven.org/maven2/org/sonatype/spice/spice-parent/12/spice-parent-12.pom

    Downloading: http://repo1.maven.org/maven2/org/sonatype/forge/forge-parent/4/forge-parent-4.pom

    Downloading: http://repo1.maven.org/maven2/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.pom

    Downloading: http://repo1.maven.org/maven2/commons-lang/commons-lang/2.5/commons-lang-2.5.jar
    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-exec/1.0.1/commons-exec-1.0.1.jar


    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-io/1.3.2/commons-io-1.3.2.jar

    [INFO] [clojure:compile {execution: compile-clojure}]
    [INFO] [clojure:test {execution: test-clojure}]

    Testing com.theoryinpractise.clojure.testrunner

    Ran 0 tests containing 0 assertions.
    0 failures, 0 errors.
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-settings/2.0/maven-settings-2.0.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.4/maven-reporting-api-2.0.4.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.4/maven-reporting-2.0.4.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven/2.0.4/maven-2.0.4.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-xhtml/1.0-alpha-11/doxia-module-xhtml-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-modules/1.0-alpha-11/doxia-modules-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia/1.0-alpha-11/doxia-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.4.5/plexus-utils-1.4.5.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-core/1.0-alpha-11/doxia-core-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-sink-api/1.0-alpha-11/doxia-sink-api-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-decoration-model/1.0-alpha-11/doxia-decoration-model-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-sitetools/1.0-alpha-11/doxia-sitetools-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-site-renderer/1.0-alpha-11/doxia-site-renderer-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-i18n/1.0-beta-7/plexus-i18n-1.0-beta-7.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-components/1.1.12/plexus-components-1.1.12.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-velocity/1.1.7/plexus-velocity-1.1.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/velocity/velocity/1.5/velocity-1.5.pom

    Downloading: http://repo1.maven.org/maven2/commons-collections/commons-collections/3.1/commons-collections-3.1.pom

    Downloading: http://repo1.maven.org/maven2/commons-lang/commons-lang/2.1/commons-lang-2.1.pom

    Downloading: http://repo1.maven.org/maven2/oro/oro/2.0.8/oro-2.0.8.pom

    Downloading: http://repo1.maven.org/maven2/commons-collections/commons-collections/3.2/commons-collections-3.2.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-apt/1.0-alpha-11/doxia-module-apt-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-fml/1.0-alpha-11/doxia-module-fml-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-xdoc/1.0-alpha-11/doxia-module-xdoc-1.0-alpha-11.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/shared/maven-doxia-tools/1.0.1/maven-doxia-tools-1.0.1.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/shared/maven-shared-components/9/maven-shared-components-9.pom

    Downloading: http://repo1.maven.org/maven2/commons-io/commons-io/1.4/commons-io-1.4.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/commons/commons-parent/7/commons-parent-7.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/1.0-alpha-7/plexus-archiver-1.0-alpha-7.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-components/1.1.6/plexus-components-1.1.6.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus/1.0.8/plexus-1.0.8.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.2/plexus-utils-1.2.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus/1.0.5/plexus-1.0.5.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.5.1/plexus-utils-1.5.1.pom

    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/jetty/6.1.5/jetty-6.1.5.pom

    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/project/6.1.5/project-6.1.5.pom

    Downloading: http://snapshots.repository.codehaus.org/org/mortbay/jetty/jetty-util/6.1.5/jetty-util-6.1.5.pom
    [INFO] Unable to find resource 'org.mortbay.jetty:jetty-util:pom:6.1.5' in repository codehaus.org (http://snapshots.repository.codehaus.org)
    Downloading: http://people.apache.org/repo/m2-snapshot-repository//org/mortbay/jetty/jetty-util/6.1.5/jetty-util-6.1.5.pom
    [INFO] Unable to find resource 'org.mortbay.jetty:jetty-util:pom:6.1.5' in repository apache.m2.incubator (http://people.apache.org/repo/m2-snapshot-repository/)
    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/jetty-util/6.1.5/jetty-util-6.1.5.pom

    Downloading: http://snapshots.repository.codehaus.org/org/mortbay/jetty/servlet-api-2.5/6.1.5/servlet-api-2.5-6.1.5.pom
    [INFO] Unable to find resource 'org.mortbay.jetty:servlet-api-2.5:pom:6.1.5' in repository codehaus.org (http://snapshots.repository.codehaus.org)
    Downloading: http://people.apache.org/repo/m2-snapshot-repository//org/mortbay/jetty/servlet-api-2.5/6.1.5/servlet-api-2.5-6.1.5.pom
    [INFO] Unable to find resource 'org.mortbay.jetty:servlet-api-2.5:pom:6.1.5' in repository apache.m2.incubator (http://people.apache.org/repo/m2-snapshot-repository/)
    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/servlet-api-2.5/6.1.5/servlet-api-2.5-6.1.5.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.5.1/plexus-utils-1.5.1.jar
    Downloading: http://repo1.maven.org/maven2/oro/oro/2.0.8/oro-2.0.8.jar
    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/jetty/6.1.5/jetty-6.1.5.jar
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/shared/maven-doxia-tools/1.0.1/maven-doxia-tools-1.0.1.jar
    Downloading: http://repo1.maven.org/maven2/org/apache/velocity/velocity/1.5/velocity-1.5.jar


    Downloading: http://repo1.maven.org/maven2/commons-lang/commons-lang/2.1/commons-lang-2.1.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-xhtml/1.0-alpha-11/doxia-module-xhtml-1.0-alpha-11.jar

    Downloading: http://repo1.maven.org/maven2/commons-io/commons-io/1.4/commons-io-1.4.jar
    Downloading: http://repo1.maven.org/maven2/commons-collections/commons-collections/3.2/commons-collections-3.2.jar


    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-i18n/1.0-beta-7/plexus-i18n-1.0-beta-7.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-core/1.0-alpha-11/doxia-core-1.0-alpha-11.jar

    Downloading: http://snapshots.repository.codehaus.org/org/mortbay/jetty/jetty-util/6.1.5/jetty-util-6.1.5.jar


    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-velocity/1.1.7/plexus-velocity-1.1.7.jar
    [INFO] Unable to find resource 'org.mortbay.jetty:jetty-util:jar:6.1.5' in repository codehaus.org (http://snapshots.repository.codehaus.org)
    Downloading: http://people.apache.org/repo/m2-snapshot-repository//org/mortbay/jetty/jetty-util/6.1.5/jetty-util-6.1.5.jar
    [INFO] Unable to find resource 'org.mortbay.jetty:jetty-util:jar:6.1.5' in repository apache.m2.incubator (http://people.apache.org/repo/m2-snapshot-repository/)
    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/jetty-util/6.1.5/jetty-util-6.1.5.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-decoration-model/1.0-alpha-11/doxia-decoration-model-1.0-alpha-11.jar


    Downloading: http://snapshots.repository.codehaus.org/org/mortbay/jetty/servlet-api-2.5/6.1.5/servlet-api-2.5-6.1.5.jar
    [INFO] Unable to find resource 'org.mortbay.jetty:servlet-api-2.5:jar:6.1.5' in repository codehaus.org (http://snapshots.repository.codehaus.org)
    Downloading: http://people.apache.org/repo/m2-snapshot-repository//org/mortbay/jetty/servlet-api-2.5/6.1.5/servlet-api-2.5-6.1.5.jar

    [INFO] Unable to find resource 'org.mortbay.jetty:servlet-api-2.5:jar:6.1.5' in repository apache.m2.incubator (http://people.apache.org/repo/m2-snapshot-repository/)
    Downloading: http://repo1.maven.org/maven2/org/mortbay/jetty/servlet-api-2.5/6.1.5/servlet-api-2.5-6.1.5.jar
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-site-renderer/1.0-alpha-11/doxia-site-renderer-1.0-alpha-11.jar
    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/1.0-alpha-7/plexus-archiver-1.0-alpha-7.jar



    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-apt/1.0-alpha-11/doxia-module-apt-1.0-alpha-11.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-fml/1.0-alpha-11/doxia-module-fml-1.0-alpha-11.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/doxia/doxia-module-xdoc/1.0-alpha-11/doxia-module-xdoc-1.0-alpha-11.jar

    [INFO] [site:attach-descriptor {execution: default-attach-descriptor}]
    [INFO] ------------------------------------------------------------------------
    [INFO] Building Unnamed - org.clojure.contrib:def:jar:1.3.0-SNAPSHOT
    [INFO]    task-segment: [package]
    [INFO] ------------------------------------------------------------------------
    [INFO] [enforcer:enforce {execution: enforce-maven}]
    [INFO] [build-helper:add-source {execution: add-clj-source}]
    [INFO] Source directory: /Users/sly/src/clojure/clojure-contrib/modules/def/src/main/clojure added.
    [INFO] [resources:resources {execution: default-resources}]
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] Copying 1 resource
    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler-api/1.5.3/plexus-compiler-api-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler/1.5.3/plexus-compiler-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler-manager/1.5.3/plexus-compiler-manager-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler-javac/1.5.3/plexus-compiler-javac-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compilers/1.5.3/plexus-compilers-1.5.3.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.0.5/plexus-utils-1.0.5.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.0.4/plexus-utils-1.0.4.jar

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler-api/1.5.3/plexus-compiler-api-1.5.3.jar

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler-manager/1.5.3/plexus-compiler-manager-1.5.3.jar

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-compiler-javac/1.5.3/plexus-compiler-javac-1.5.3.jar

    [INFO] [compiler:compile {execution: default-compile}]
    [INFO] Nothing to compile - all classes are up to date
    [INFO] [clojure:compile {execution: compile-clojure}]
    Compiling clojure.contrib.def to /var/folders/bF/bFw21j1PEYOaj7H8Xz3snk+++Tc/-Tmp-/classes564930293474587356.dir
    [INFO] [resources:testResources {execution: default-testResources}]
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] skip non existing resourceDirectory /Users/sly/src/clojure/clojure-contrib/modules/def/src/test/resources
    [INFO] [compiler:testCompile {execution: default-testCompile}]
    [INFO] No sources to compile
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/surefire/surefire-booter/2.4.3/surefire-booter-2.4.3.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/surefire/surefire-api/2.4.3/surefire-api-2.4.3.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-toolchain/1.0/maven-toolchain-1.0.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/surefire/surefire-booter/2.4.3/surefire-booter-2.4.3.jar

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/surefire/surefire-api/2.4.3/surefire-api-2.4.3.jar

    [INFO] [surefire:test {execution: default-test}]
    [INFO] No tests to run.
    [INFO] [clojure:test {execution: test-clojure}]

    Testing clojure.contrib.test-def

    Ran 1 tests containing 2 assertions.
    0 failures, 0 errors.
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-project/2.0.7/maven-project-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven/2.0.7/maven-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-settings/2.0.7/maven-settings-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-model/2.0.7/maven-model-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-profile/2.0.7/maven-profile-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-artifact-manager/2.0.7/maven-artifact-manager-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-repository-metadata/2.0.7/maven-repository-metadata-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-artifact/2.0.7/maven-artifact-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-plugin-registry/2.0.7/maven-plugin-registry-2.0.7.pom

    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-archiver/2.3/maven-archiver-2.3.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/1.0-alpha-9/plexus-archiver-1.0-alpha-9.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-15/plexus-container-default-1.0-alpha-15.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-containers/1.0-alpha-15/plexus-containers-1.0-alpha-15.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-component-api/1.0-alpha-15/plexus-component-api-1.0-alpha-15.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-classworlds/1.2-alpha-6/plexus-classworlds-1.2-alpha-6.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-io/1.0-alpha-1/plexus-io-1.0-alpha-1.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-component-api/1.0-alpha-16/plexus-component-api-1.0-alpha-16.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-containers/1.0-alpha-16/plexus-containers-1.0-alpha-16.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.4.9/plexus-utils-1.4.9.pom

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/1.4.9/plexus-utils-1.4.9.jar
    Downloading: http://repo1.maven.org/maven2/org/apache/maven/maven-archiver/2.3/maven-archiver-2.3.jar

    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-archiver/1.0-alpha-9/plexus-archiver-1.0-alpha-9.jar


    Downloading: http://repo1.maven.org/maven2/org/codehaus/plexus/plexus-io/1.0-alpha-1/plexus-io-1.0-alpha-1.jar

    [INFO] [jar:jar {execution: default-jar}]
    [INFO] Building jar: /Users/sly/src/clojure/clojure-contrib/modules/def/target/def-1.3.0-SNAPSHOT.jar
    [INFO] ------------------------------------------------------------------------
    [INFO] Building Unnamed - org.clojure.contrib:types:jar:1.3.0-SNAPSHOT
    [INFO]    task-segment: [package]
    [INFO] ------------------------------------------------------------------------


What in the world is all of this stuff? A hodgepodge of poms and jars of things of which I've never heard and would just as soon avoid. What _is_ plexus? Doxia? Wagon? Commons? Do I even want to know? Are these dependencies for clojure-contrib itself or for the process of managing the building/jaring/deploying (whatever that means!)/etc... clojure-contrib? I think there's some stuff in clojure-contrib I want to use, but do I _really_ need all of this? How would I know? I also understand that there has been an effort to split clojure-contrib up into various components pieces, but that there might be an effort underway to undo that previous effort. It's all a bit of a mess.

--
