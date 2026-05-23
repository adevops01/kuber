To view the available parameters that can be used with the tool, run:

sh /root/Assessor/Assessor-CLI.sh  -h

Run the test in interactive mode and use the following settings:

Benchmarks/Data-Stream Collections: CIS Ubuntu Linux 24.04 LTS Benchmark v1.0.0
Profile : Level 1 - Server

Use sh /root/Assessor/Assessor-CLI.sh -h to see all available options. Utilize the following options as per the task guidelines:

-i: interactive mode
-rd: location in which the output report will be saved
-nts: timestamps will not be appended to the report name
-rp: report name prefix. .html will be automatically appended to the name provided
After the report generation is complete, click on Assessment Report tab to see the report. You may need to reload the page if the updates are not automatically loaded.

To run the report:

`sh /root/Assessor/Assessor-CLI.sh -i -rd /var/www/html/ -nts -rp index`
Use the following parameters when prompted:

Benchmarks/Data-Stream Collections: CIS Ubuntu Linux 24.04 LTS Benchmark v1.0.0
Profile: Level 1 - Server
After the report generation is complete, click on Assessment Report tab to see the report. You may need to reload the page if the updates are not automatically loaded.
