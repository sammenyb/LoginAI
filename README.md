## DBSCAN On SSO Login dataset
### Dataset taken from https://github.com/das-group/rba-dataset

### Project made by Samuel Nyberg


## Getting Started
Because Github limits the size of a repository and the dataset is large I decided to do a .gitignore and not include the dataset or training data.
To run this Model yourself, please download the dataset from the orgin: https://github.com/das-group/rba-dataset

When its downloaded, in main.ipynb change this row:  
to_csv_batch('rba-dataset.csv', 'Batches'), to the right path to the dataset.  

I've developed this in python version 3.11.5.  
Make sure to have the following libraries installed:  
Pandas, Sklearn, Numpy


## Overview

### Original Dataset

The data set contains the following features related to each login
attempt on the SSO:


Feature                    | Data Type | Description                                                                                      | Range or Example
---------------------------|-----------|--------------------------------------------------------------------------------------------------|------------------------------------------------------
IP Address                 | String    | IP address belonging to the login attempt                                                        | 0.0.0.0 - 255.255.255.255
Country                    | String    | Country derived from the IP address                                                              | US
Region                     | String    | Region derived from the IP address                                                               | New York
City                       | String    | City derived from the IP address                                                                 | Rochester
ASN                        | Integer   | Autonomous system number derived from the IP address                                             | 0 - 600000
User Agent String          | String    | User agent string submitted by the client                                                        | Mozilla/5.0 (Windows NT 10.0; Win64; \...
OS Name and Version        | String    | Operating system name and version derived from the user agent string                             | Windows 10
Browser Name and Version   | String    | Browser name and version derived from the user agent string                                      | Chrome 70.0.3538
Device Type                | String    | Device type derived from the user agent string                                                   | (`mobile`, `desktop`, `tablet`, `bot`, `unknown`)[^1]
User ID                    | Integer   | Idenfication number related to the affected user account                                         | [Random pseudonym]
Login Timestamp            | Integer   | Timestamp related to the login attempt                                                           | [64 Bit timestamp]
Round-Trip Time (RTT) [ms] | Integer   | Server-side measured latency between client and server                                           | 1 - 8600000
Login Successful           | Boolean   | `True`: Login was successful, `False`: Login failed                                              | (`true`, `false`)
Is Attack IP               | Boolean   | IP address was found in known attacker data set                                                  | (`true`, `false`)
Is Account Takeover        | Boolean   | Login attempt was identified as account takeover by incident response team of the online service | (`true`, `false`)

[^1]: Few (invalid) user agents strings from the original data set could not be parsed, so their device type is empty. Perhaps this parse error is useful information for your studies, so we kept these 1526 entries.  
  
  


### Processed Dataset

This modified dataset is converted to a numerical format so that the DBSCAN model can process it properly. 
A combination of cyclic encoding, frequency encoding was used. 

Feature                    | Data Type | Description                                                                                      | Number Range
---------------------------|-----------|--------------------------------------------------------------------------------------------------|------------------------------------------------------
ASN                        | Integer   | Autonomous system number derived from the IP address                                             | 0 - 600000
hour                       | Integer   | The hour of the day                                                                              | 0 - 24
minute                     | Integer   | The minute of the hour                                                                           | 0 - 60
second                     | Integer   | The second of the minute                                                                         | 0 - 60
day                        | Integer   | The day of the month                                                                             | 0 - 31
month                      | Integer   | The month of the year                                                                            | 0 - 12
year                       | Integer   | The year                                                                                         | 2020 - 2021
ip_octlet1                 | Integer   | The first octlet of an ip-adress, in 192.168.0.1 the 192 is the first octlet                     | 0 - 255
ip_octlet2                 | Integer   | The first octlet of an ip-adress, in 192.168.0.1 the 168 is the first octlet                     | 0 - 255
ip_octlet3                 | Integer   | The first octlet of an ip-adress, in 192.168.0.1 the 0 is the first octlet                       | 0 - 255
ip_octlet4                 | Integer   | The first octlet of an ip-adress, in 192.168.0.1 the 1 is the first octlet                       | 0 - 255
country_freq               | Integer   | Number-labeling counties based on the frequency they occur in the data.                          | 0 - highest frequency
city_freq                  | Integer   | Number-labeling cities based on the frequency they occur in the data.                            | 0 - highest frequency
region_freq                | Integer   | Number-labeling regions based on the frequency they occur in the data.                           | 0 - highest frequency
device_type_freq           | Integer   | Number-labeling the device types based on the frequency they occur in the data.                  | 0 - highest frequency
os_name_freq               | Integer   | Number-labeling the OS names based on the frequency they occur in the data.                      | 0 - highest frequency
os_version_freq            | Integer   | Number-labeling the OS versions based on the frequency they occur in the data.                   | 0 - highest frequency
user_agent_device_freq     | Integer   | Number-labeling the device type based on the frequency they occur in the data.                   | 0 - highest frequency
browser_name_freq          | Integer   | Number-labeling browser names based on the frequency they occur in the data.                     | 0 - highest frequency
browser_version_freq       | Integer   | Number-labeling browser versions based on the frequency they occur in the data.                  | 0 - highest frequency
login_successful           | Integer   | 1: Login was successful, 0: Login failed                                                         | 0 - 1
is_attack_ip               | Integer   | IP address was found in known attacker data set                                                  | 0 - 1
is_account_takeover        | Integer   | Login attempt was identified as account takeover by incident response team of the online service | 0 - 1






## License

This data set and the contents of this repository are licensed under the
[Creative Commons Attribution 4.0 International (CC BY 4.0)] license.
See the [LICENSE](LICENSE) file for details.  If the data set is used
within a publication, the following journal article has to be cited as
the source of the data set:

Stephan Wiefling, Paul René Jørgensen, Sigurd Thunem, and Luigi Lo
Iacono: Pump Up Password Security! Evaluating and Enhancing Risk-Based
Authentication on a Real-World Large-Scale Online Service. In: ACM
Transactions on Privacy and Security (2022). doi: [10.1145/3546069](https://doi.org/10.1145/3546069)



[Pump Up Password Security! Evaluating and Enhancing Risk-Based Authentication on a Real-World Large-Scale Online Service]: https://doi.org/10.1145/3546069
[Risk-Based Authentication (RBA)]: https://riskbasedauthentication.org
[Freeman et al. (2016)]: https://doi.org/10.14722/ndss.2016.23240
[Creative Commons Attribution 4.0 International (CC BY 4.0)]: https://creativecommons.org/licenses/by/4.0/