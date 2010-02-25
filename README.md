NSM Addon Updater 1.0.0a1
=========================

Written by: Leevi Graham, Technical Director of Newism, based on LG Addon Updater (EE1.x)

NSM Addon Updater is an EE 2.0 accessory that checks an external RSS feed for version updates and displays them in your extension admin.

If you want to include NSM Addon updater support in your addon follow these simple steps:

1. Create a config.php file in your addon folder
2. Add: `config['nsm_addon_updater']['versions_xml'] = 'http://your_domain/versions.xml`

The url should point to a valid RSS 2.0 XML feed that lists individual versions of your addon as <items>. There is only one required addition to a standard feed: `<ee_addon:version>1.0.0b1</ee_addon:version>` which is used for version comparison.

Each feed is individually cached so that the CURL calls don't stall the loading of the CP. Additionally the calls are made via AJAX so there should be no negative affect on CP load.

Example RSS 2.0 XML Feed
------------------------

	<?xml version="1.0" encoding="utf-8"?>
	<rss version="2.0" xmlns:ee_addon="http://expressionengine-addons.com/nsm_addon_updater/#rss-xml">
		<channel>
			<title>NSM Addon Updater Changelog</title>
			<link>http://yourdomain.com/nsm.addon_updater.ee_addon/appcast.xml</link>
			<description>Most recent changes with links to updates.</description>
			<item>
				<title>Version 1.0.0b1</title>
				<!-- Additional tag required for NSM Addon Updater -->
				<ee_addon:version>1.0.0b1</ee_addon:version>
				<link>http://yourdomain.com/nsm.addon_updater.ee_addon/1.0.0b1/</link>
				<pubDate>Wed, 09 Jan 2006 19:20:11 +0000</pubDate>
				<description><![CDATA[
					<ul>
						<li>Added the {selected_group_id} variable for available use in the User Key Notification Template.</li>
						<li>Added the form:attribute="" parameter type to all User functions that output forms.</li>
					</ul>
				]]>
				</description>
				<enclosure url="http://yourdomain.com/nsm.addon_updater.ee_addon/download.zip?version=1.0.0b1" length="1623481" type="application/zip" />
			 </item>
		</channel>
	</rss>
