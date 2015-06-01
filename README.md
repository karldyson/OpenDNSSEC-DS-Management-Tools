A set of tools that you can use to automate KSK rollover in conjunction with OpenDNSSEC

Initially, I've written tools for use with Gandi


== gandi-publish-ds ==

Can specified in <DelegatedSignerSubmitCommand> in /etc/opendnssec/conf.xml

Takes input as provided by OpenDNSSEC and publishes DS to via Gandi API.

Requires config file in one of (later overrides earlier):

  * /etc/gandi.conf
  * /usr/local/etc/gandi.conf
  * ~/.gandrc

Config file format looks like:

apikey 429769428649hkasjh<br/>
endpoint https://rpc.gandi.net/xmlrpc/


== check-for-ds-seen ==

Designed to run from cron.

Looks for keys that are "waiting for ds seen" status and checks all locatable nameservers
looking for the DS record.
Exits upon first NS that DOESN'T have the DS.
If all NS have the DS, then ods-ksmutil key ds-seen is executed for the domain & keytag


== gandi-remove-dead-keys ==

Designed to run from cron.

Looks for KSK that are dead, and pulls them from the Gandi API

Uses the same config file as gandi-publish-ds, of course.



== TODO ==

* Have gandi-publish-ds email someone with what it did.
	(the other two will output which can email to the cron owner/mail recipient)
