# osgi-springboot
1. Description

osgi-* is java project
osgi.* is plugin project

osgi-spellcheck-bridge and osgi-spellcheck-interface are two plain java jar files. These two files will be used not only for SpringBoot but also for eclipse osgi bundles

osgi-spellcheck-web is SpringBoot application

osgi.spellcheck.api.wrapper is real implementation of spellcheck functions. The real function is provided by osgi bundles

osgi.spellcheck.bridge.extensionbundle and osgi.spellcheck.extensionbundle are extracted from framework launcher so that these plugins can start when equinox startups.

osgi.spellcheck.bridge.wrapper is a plugin project and wrapps the SpellcheckBridge of osgi-spellcheck-bridge into bundle so that the other bundles can call it in their own context. It depends on osgi-spellcheck-bridge jar during building process. In runtime it will use the SpellcheckBridge loaded by Spring framework class loader. 

osgi.spellcheck.spellchecker is a plugin project and wrapps the ISpellcheck and SpellCheckResult into bundle so that the other bundles can call it in their own context. It depends on osgi-spellchck-interface jar during building process. In runtime it will use the SpellcheckBridge loaded by Spring framework class loader. osgi.spellcheck.api.wrapper depends on this plugin project

2. Build

2.1 build eclipse plugins with gradle
2.2 add eclipse folde to docker image
2.3 after jar file is out, put pluign jar file to eclipse folder in docker image and set the SPELLCHECK_OSGI variable which will be used by spring boot application to load equinox

3. Detail interaction please refer to the source code in zip file and BridgeServlet.java in eclipse source
