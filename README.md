sa-logwatch
===========

Implementation of the logwatch - handy script that would mail you overview for your system

[![Build Status](https://travis-ci.org/softasap/sa-logwatch.svg?branch=master)](https://travis-ci.org/softasap/sa-logwatch)


Logwatch is a log parsing program that analyzes and generates daily reports on your system’s log activity. Logwatch does not provide real time alerts, but instead will create a digest organized by systems for ease of review. More advanced users can also pair Logwatch with custom analysis scripts to fine-tune their reports

Important: by default package would try to install local mail server, thus we would recommend to install & configure it on your own,
for example, via sa-postfix role.


Example of use: check box-example

Simple:

```YAML

     - {
         role: "sa-postfix"
       } 
     - {
         role: "sa-logwatch"
       }

```


Advanced:

```YAML

logwatch_mail_to: "root@localhost"  # Email Address which Logwatch reports to                                                                                                                               
logwatch_detail: "low"            # The level of detail in the Logwatch report
logwatch_range: "yesterday"       # The default time range for the Logwatch report
logwatch_output: "stdout"         # The output method of the Logwatch report
logwatch_format: "text"           # The format of the Logwatch report

logwatch_conf_custom_props:
   - {regexp: '^[#]?Output =.*', line: 'Output = {{logwatch_output}}'}
   - {regexp: '^[#]?Format =.*', line: 'Format = {{logwatch_format}}'}                                                                                                                                      
   - {regexp: '^[#]?Range =.*', line: 'Range = {{logwatch_range}}'}
   - {regexp: '^[#]?Detail =.*', line: 'Detail = {{logwatch_range}}'}
   - {regexp: '^[#]?MailTo =.*', line: 'MailTo = {{logwatch_mail_to}}'}


```

```YAML

     - {
         role: "sa-postfix"
       }


     - {
         role: "sa-logwatch",
         logwatch_mail_to: "root@localhost",  # Email Address which Logwatch reports to
         logwatch_detail: "low",            # The level of detail in the Logwatch report
         logwatch_range: "yesterday",       # The default time range for the Logwatch report
         logwatch_output: "stdout",         # The output method of the Logwatch report
         logwatch_format: "text"           # The format of the Logwatch report
       }

```

```YAML

     - {
         role: "sa-postfix"
       }


     - {
         role: "sa-logwatch",
         logwatch_conf_props: "{{logwatch_conf_custom_props}}"
       }


```


To view logwatch output use less :
```bash
sudo logwatch | less
```

To email a logwatch report for the past 7 days to an email address, enter the following and replace mail@domain.com with the required email:

```bash
sudo logwatch --mailto mail@domain.com --output mail --format html --range 'between -7 days and today' 
```


Copyright and license
---------------------


Code licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) or the [MIT License] (http://opensource.org/licenses/MIT).

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)
