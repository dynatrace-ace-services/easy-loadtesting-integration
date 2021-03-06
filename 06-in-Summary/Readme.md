 # 06-in-Summary 
it's what you can import in your Jenkins pipeline to automate your monitoring 
      
- stop loadgen
      
      docker-compose stop loadgen

- export the variables

      export NEW_CLI=1;
      export MyTenant=https://abcd.live.dynatrace.com
      export MyToken=ABCD123456XYZ
      export Appname=<Host_Group>
      export Hostname=<myhostname.domaine.com>


- update the config

      cd;
      cd easy-loadtesting-integration;
      git pull;
      cp test-plan-* ../docker-jmeter/tests/

-  deploy the config

       ./monaco deploy -e=environments.yaml 01-deploy-config-with-Monaco/step1;
       ./monaco deploy -e=environments.yaml 01-deploy-config-with-Monaco/step2;
       ./monaco deploy -e=environments.yaml 04-driven-Slo/Metric;
       ./monaco deploy -e=environments.yaml 04-driven-Slo/Slo;
      
- run the load test 
      
      cd;
      cd docker-jmeter;
      ./run.sh  -n -t tests/test-plan-with-integration.jmx -Jtenant=$MyTenant -Jtoken=$MyToken -Jhostname=$Hostname -l tests/loadest.jlt
  
 # Next Step
- [07-next-Step](https://github.com/dynatrace-ace-services/easy-loadtesting-integration/tree/main/07-next-Step) => now you are ready to integrate Dynatrace configuration to your CICD pipeline.
