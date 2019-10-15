# dBnk Addons Contract (dbnk-addons-contract)
dBnk Addons function alongside a separate [Arisen](https://arisen.network)-based smart contract called [dbnk-addons](https://github.com/dbnks/dbnk-addons-contract), although dBnk's Addons Marketplace still utilizes the [dbnk](https://github.com/dbnks/dbnk-contract) for accessing certain data and completing specific application-specific operations. 

## Contract Scopes
The following "SCOPES" are included with the ```dbnk-addons-contract```.

- ```listings``` - ***Lists addons in the dBnk ecosystem.***
- ```reviews``` - ***Lists reviews by addon.***
- ```blacklist``` - ***Lists addons that have been blacklisted.***
- ```installations``` - ***Lists entire installation history of all addons on a per-user basis.***
- ```reports``` - ***Lists user reporting information regarding specific addons.***

### Listing Scope 
The ```listing``` scope is used to store dBnk Addon Marketplace listings and the data associated with them. The ```listing``` scope uses several datasets to list addons using both on-chain ( [Arisen](https://github.com/arisenio/technical-whitepaper) ) and off-chain ( [dWeb](https://github.com/distributedweb/whitepaper) ) resources. 

The ```listing``` scope includes the following items:
- ```addon_name``` ***(string)*** - A string of the addon's displayed name.
- ```addon_category``` ***(string)*** - A string that reflects many of the Addon Marketplace's categories (i.e. accounting, debit cards, merchant services, etc).
- ```addon_price``` ***(integer)*** - An integer that reflects the price of an addon. Must be shown in a valid RSN-based format.
- ```addon_dweb_hash``` ***(string)*** - The dWeb URL (Hash URL) to where the addon is hosted on the dWeb. 
- ```peeps_developer``` ***(string)*** - The Peeps' Developer's username that created the addon. It's important to note that a Peeps Developer's username is nothing but an Arisen blockchain-based account, just as an dBnk username is also an Arisen blockchain-based account. In fact, an dBnk user can create a [Peeps Developer Account](https://developers.dpeeps.com) using their dBnk username or vice versa. An Arisen blockchain account can be used to login to any Peeps-based dApps like dBnk or even the Peeps Developer Dashboard itself. Once an Arisen blockchain account has been created, it can be used to login to any application that uses Arisen's blockchain for authentication. It's also important to note, that ```peeps_developer``` correlates to the ```developer``` SCOPE within the [peeps-developer-contract](https://github.com/dpeeps/peeps-developer-contract). 
- ```addon_description``` ***(string)*** - A string that reflects a short description of the addon itself. Limited to 1500 characters.
- ```addon_logo``` ***(string)*** - A string of a dWeb hash where the logo is stored off-chain. When uploading a logo for an addon, it should be placed in a dDrive on the dWeb and linked via ```addon_logo```. Example: ```<dweb-key>/logo.png```
- ```addon_header``` ***(string)*** - A string of a dWeb hash where the addon's header image is stored off-chain. The addon header is used as a customizable background image on an addon's page in the dBnk Addon Marketplace. 
-```addon_created``` ***(integer)*** - An integer that reflects the precise timestamp of when the addon was listed. In other words, when this listing within the ```listings``` scope was created.

**NOTE:** ***All addons must be listed through the Peeps Developer Dashboard as an ```dbnk-addon```, so that it ends up in the dBnk Addon Marketplace.***

**IMPORTANT:** ***Developers are paid in RSN for paid addons, directly to their Arisen-based dBnk account (this is the account reflected by their ```peeps_developer``` username.***

### Reviews Scope
The ```reviews``` scope is designed to allow dBnk to have a fully decentralized review system for addons. Below are explanations of the options within the SCOPE itself. 

```addon_name``` ***(string)*** -  A string of the name of the addon being reviewed.
```review_rating``` ***(integer)*** - An integer reflecting the rating. The integer should reflect a range of 0-5. Within dBnk's application, this value is averaged with other ratings for the same addon and displayed as a star-rating.
```review_content``` ***(string)*** - A string of the actual review text written by the reviewer. This is limited to 500 characters.
```review_time``` ***(integer)*** - An integer that reflects the precise timestamp of when this review was added to the ledger.
```dbnk_user``` ***(string)*** - A string representing the dBnk user that is creating this review.

### Reports Scope
Reports are meant to bring to life certain decentralized methods of policing malicious addons within dBnk. Using dBnk's policing algorithms and reporting data, malicious addons can be blacklisted automatically through the blacklist scope. dBnk's policing algorithms are explained within the [dBnk Blueprint](https://github.com/dbnks/dbnk/master/blob/BLUEPRINT.md). In short, the ```reports``` SCOPE uses the ```report_type``` to understand why an addon is being reported. Options include "malicious, not working, illegal content, spam and emergency". Reports are weighted differently on a user-by-user basis, where users who have large RSN holdings and their reports, makes it more likely that the system will blacklist the addon being reported.

Below are a description of the options within the SCOPE itself:

```addon_name``` ***(string)*** - A string of the name of the addon being reported.
```dbnk_user``` ***(string)*** - A string of the dBnk user who is making the report.
```report_type``` ***(string)*** - A string of the type of report (i.e. malicious, not working, spam, etc.).

### Blacklist Scope
The blacklists scope can only be written to by the dApp itself, when reports via the ```reports``` SCOPE and the dBnk's policing algorithms decide it's appropriate to blacklist an addon. 

Below are a description of the options within the SCOPE itself:

```blacklist_date``` ***(integer)*** - An integer that refers to a precise timestamp of when the blacklist was recorded on the ledger.
```addon_name``` ***(string)*** - A string of the ```addon_name``` that is being blacklisted.

Once blacklisted, an addon is completely and permanently blacklisted by the dBnk community and there is no recourse for being reinstated to the ```dBnk Addon Marketplace```.

### Installations Scope
The installations SCOPE is used to show which  ```dbnk_user``` has installed a particular addon globally (on-chain). Installations are counted through the ```installations``` SCOPE and dBnk's application is able to show which addons are installed for a particular dBnk user by storing the information publicly on the ledger. This means an addon installed via dBnk Mobile, will automatically show as an installed addon via dBnk Desktop, since the installation data is stored outside the device (on-chain) and since all dBnk addons are essentially decentralized web applications themselves, hosted P2P over the dWeb protocol (off-chain), they are not located on the device they're being accessed on either. Rather, the "Addon Viewer Window" is basically a dWeb browser that resolves each addon via a dWeb hash (stored in the ```listings``` SCOPE).

The ```installations``` SCOPE contains the following options:

```addon_name``` ***(string)*** - A string of the addon name that is being installed.
```dbnk_user``` ***(string)*** - A string of the dBnk user who is initiating the installation.
```status``` ***(boolean)*** - A boolean of the addon's installation status (i.e true if installed)

## You Can Contribute
dBnk is a grassroots software project that anyone can contribute to. Whether you're looking to fix bugs, add features, design UI components or even offer up a new translation, all contributions are welcomed. If you would like to contribute, please join the [Peeps Development Channel](https://t.me/peepsdev) on Telegram and let our community of developers know that you would like to contribute to dBnk's development, as well a what you'd like to contribute to the project itself.

## Contributors
[Jared Rice Sr.](jared@dpeeps.com)
[NMH](nmh@dpeeps.com)
[M](m@dpeeps.com)
[Graham](g@dpeeps.com)
[Michael Taggart](michael@dpeeps.com)

## LICENSE
```dbnk-addons-contract``` is covered under the [MIT LICENSE](LICENSE.md) and is a copyright of [Peeps](https://dpeeps.com).

## Important
See LICENSE for copyright and license terms. Peeps makes its contribution on a voluntary basis as a member of the Arisen and dBnk communities and is not responsible for ensuring the overall performance of the software or any related applications. We make no representation, warranty, guarantee or undertaking in respect of the software or any related documentation, whether expressed or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall we be liable for any claim, damages or other liability, whether in an act ion of contract, tort or otherwise, arising from, out of or in connection with the software or documentation or the user or other dealings in the software or documentation. Any test results or performance figures are indicative and will not reflect performance under all conditions. Any reference to any third party or third-party product, service or other resource is not an endorsement  or recommendation by Peeps. We are not responsible, and disclaim any and all responsibility and liability, for your user of or reliance on any of these resources. Third-party resources may be updated, changed or terminated at any time, so the information here may be out of date or inaccurate. Any person using or offering this software in connect ion with providing software, goods or services to third parties shall advise such third parties of these license terms, disclaimers and exclusions of liability. Peeps, Peeps Labs, dBnk, Arisen and associated logos are copyright of Peeps. 

Wallets and related components are complex software that requires the highest levels of security. If incorrectly built or used, they may compromise users' private keys and digital assets. Wallet applications and related components should undergo thorough security evaluations before being used. Only experienced developers should work with this software.
