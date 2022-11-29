---
annotation-target::designing_data_intensive_applications.pdf
---




>%%
>```annotation-json
>{"created":"2022-11-28T22:04:38.004Z","text":"Failure and Fault are not the same.","updated":"2022-11-28T22:04:38.004Z","document":{"title":"Designing Data-Intensive Applications","link":[{"href":"urn:x-pdf:f4030ab3256cbd6de727d8a4f1de8630"},{"href":"vault:/Computer_Science/designing_data_intensive_applications.pdf"}],"documentFingerprint":"f4030ab3256cbd6de727d8a4f1de8630"},"uri":"vault:/Computer_Science/designing_data_intensive_applications.pdf","target":[{"source":"vault:/Computer_Science/designing_data_intensive_applications.pdf","selector":[{"type":"TextPositionSelector","start":52805,"end":53325},{"type":"TextQuoteSelector","exact":"Note that a fault is not the same as a failure [2]. A fault is usually defined as one com‐ponent of the system deviating from its spec, whereas a failure is when the system as awhole stops providing the required service to the user. It is impossible to reduce theprobability  of  a  fault  to  zero;  therefore  it  is  usually  best  to  design  fault-tolerancemechanisms  that  prevent  faults  from  causing  failures.  In  this  book  we  cover  severaltechniques for building reliable systems from unreliable parts.","prefix":"erating certain types of faults.","suffix":"Counterintuitively,  in  such  f"}]}]}
>```
>%%
>*%%PREFIX%%erating certain types of faults.%%HIGHLIGHT%% ==Note that a fault is not the same as a failure [2]. A fault is usually defined as one com‐ponent of the system deviating from its spec, whereas a failure is when the system as awhole stops providing the required service to the user. It is impossible to reduce theprobability  of  a  fault  to  zero;  therefore  it  is  usually  best  to  design  fault-tolerancemechanisms  that  prevent  faults  from  causing  failures.  In  this  book  we  cover  severaltechniques for building reliable systems from unreliable parts.== %%POSTFIX%%Counterintuitively,  in  such  f*
>%%LINK%%[[#^5y4kax0p2bm|show annotation]]
>%%COMMENT%%
>Failure and Fault are not the same.
>%%TAGS%%
>
^5y4kax0p2bm


>%%
>```annotation-json
>{"created":"2022-11-28T22:05:13.387Z","updated":"2022-11-28T22:05:13.387Z","document":{"title":"Designing Data-Intensive Applications","link":[{"href":"urn:x-pdf:f4030ab3256cbd6de727d8a4f1de8630"},{"href":"vault:/Computer_Science/designing_data_intensive_applications.pdf"}],"documentFingerprint":"f4030ab3256cbd6de727d8a4f1de8630"},"uri":"vault:/Computer_Science/designing_data_intensive_applications.pdf","target":[{"source":"vault:/Computer_Science/designing_data_intensive_applications.pdf","selector":[{"type":"TextPositionSelector","start":53920,"end":54394},{"type":"TextQuoteSelector","exact":"Although  we  generally  prefer  tolerating  faults  over  preventing  faults,  there  are  caseswhere  prevention  is  better  than  cure  (e.g.,  because  no  cure  exists).  This  is  the  casewith  security  matters,  for  example:  if  an  attacker  has  compromised  a  system  andgained  access  to  sensitive  data,  that  event  cannot  be  undone.  However,  this  bookmostly deals with the kinds of faults that can be cured, as described in the followingsections.","prefix":" is an example of this approach.","suffix":"Hardware FaultsWhen  we  think  "}]}]}
>```
>%%
>*%%PREFIX%%is an example of this approach.%%HIGHLIGHT%% ==Although  we  generally  prefer  tolerating  faults  over  preventing  faults,  there  are  caseswhere  prevention  is  better  than  cure  (e.g.,  because  no  cure  exists).  This  is  the  casewith  security  matters,  for  example:  if  an  attacker  has  compromised  a  system  andgained  access  to  sensitive  data,  that  event  cannot  be  undone.  However,  this  bookmostly deals with the kinds of faults that can be cured, as described in the followingsections.== %%POSTFIX%%Hardware FaultsWhen  we  think*
>%%LINK%%[[#^sp2ye3uhe|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^sp2ye3uhe
