Top DNS Measurement
===================

Overview
--------

This script uses a built in probabalistic measurement mechanism in Bro to 
measure the top DNS requests (by type of query, i.e., CNAME, A, AAAA, etc) being
done over a definable period of time.  This is logged into a new log named
"top_dns.log".

By using the probabalistic mechanism, it makes this task something that can be 
achieved in a memory efficient manner and loading this script shouldn't have 
any truly significant performance impact on most deployments.

Installation
------------

::

	bro-pkg refresh
	bro-pkg install bro/corelight/top-dns

Configuration
-------------

If you would like to change the logging/measurement interval, use the following
snippet (default is 15 minutes)::

	redef TopDNS::logging_interval = 1hr;

If you would like to log more or less than the default of 10 names for each 
query type, you can use the following snippet::

	redef TopDNS::top_k = 20;

If you would like to add something like MX recore queries to be measured, you 
can add the following snippet::

	redef TopDNS::records += {"MX"};

By default this package will measure based on the full domain.  If you'd like
measure based on trimming down to the "domain" (www.google.co.uk would be 
trimmed to google.co.uk), you can use the following snippet in local.bro::

	redef TopDNS::use_trimmed_domain = T;
