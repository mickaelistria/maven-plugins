To use this plugin in your own project:

1. Add it to your pom.xml with this:

	<build>
		<plugins>
			<plugin>
				<groupId>org.jboss.maven.plugin</groupId>
				<artifactId>hudson-job-sync-plugin</artifactId>
				<version>0.0.1-SNAPSHOT</version>
				<executions>
					<execution>
						<phase>install</phase>
						<goals>
							<goal>run</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
<!-- 
To be able to connect to server, must first import certificate or you may get this error:

	javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target

AS USER (with Firefox):

Browse to https://hudson.qa.jboss.com/hudson & accept the cert.

	Edit > Preferences > Advanced > Encryption > View Certificates > find hudson cert > Export to file /tmp/hudson.qa.jboss.com.cert

AS ROOT (default password is "changeit"):

	# /opt/sun-java2-6.0/jre/bin/keytool -list -keystore /opt/sun-java2-6.0/jre/lib/security/cacerts | grep hudson
		# (if you need to replace a cert, delete the old one first)
		# /opt/sun-java2-6.0/jre/bin/keytool -delete -alias hudson.qa -keystore /opt/sun-java2-6.0/jre/lib/security/cacerts
	# /opt/sun-java2-6.0/jre/bin/keytool -import -alias hudson.qa -keystore /opt/sun-java2-6.0/jre/lib/security/cacerts -file /tmp/hudson.qa.jboss.com.cert
	# /opt/sun-java2-6.0/jre/bin/keytool -list -keystore /opt/sun-java2-6.0/jre/lib/security/cacerts | grep hudson

To run, make sure that JAVA_HOME is set to the path where you imported the cert, eg.:

	$ export JAVA_HOME=/opt/sun-java2-6.0/; mvn clean install
-->
					<!-- more output w/ verbose; default: false -->
					<!-- <verbose>false</verbose> -->

					<!-- server and connection details -->
					<!-- <hudsonURL>https://hudson.qa.jboss.com/hudson/</hudsonURL> -->
					<hudsonURL>http://localhost:8080/</hudsonURL>
					<username>SET USERNAME HERE</username>
					<password>SET PASSWORD HERE</password>

					<!-- to select a subset of jobs, use these filters; default: view/myViewName/ -->
					<!-- <viewFilter>view/DevStudio_Stable_Branch/</viewFilter> -->
					<!-- <viewFilter>view/DevStudio_Trunk/</viewFilter> -->
					
					<!-- default .* to select all -->
					<!-- <regexFilter>.*TEMPLATE.*</regexFilter> -->
					<!-- <regexFilter>.*</regexFilter> -->
					<regexFilter>MyJobNameHere</regexFilter>

					<!-- if there's an existing config.xml (not config.$timestamp.xml) then overwrite it if true; default false -->
					<!-- <overwriteExistingConfigXMLFile>false</overwriteExistingConfigXMLFile> -->
                    
					<!-- either "pull" updated job config.xml file(s) from the server (default, reads only & stores a copy locally), or 
					            "push" updates from local to the server (replacing existing job config.xml on server :: CAUTION!)
					-->
					<!-- <operation>pull</operation> -->
					
					<!-- if pushing, can also store a copy of the latest configuration with storeSnapshotOnPush = true; default false -->
					<!-- <storeSnapshotOnPush>false</storeSnapshotOnPush> -->

				</configuration>
			</plugin>
		</plugins>
	</build>

2. To run, make sure that JAVA_HOME is set to the path where you imported the cert, eg.:

	$ export JAVA_HOME=/opt/sun-java2-6.0/; mvn clean install -f pom-sync.xml -Doperation=pull
 	
