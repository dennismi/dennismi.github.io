---
layout: post
title: "Boxstarter hacking (pt. 2)"
description: ""
category: boxstarter
tags: [boxstarter, sysadmin, powershell, trials]
---
{% include JB/setup %}
<p>So i got an answer from the boxstarter guru’s over at codeplex. Actually Matt Wrock answered himself.<br/>He told me that the code i was using like this: </p>

```posh
invoke-boxstarter {(new-object net.webclient).DownloadString('http://path/to/domainjoin.txt') | iex}  
```

<p>was calling into some lower level functions of boxstarter, hence it was a bad idea.</p>

<p>He directed me to calling  </p>

```posh
Install-BoxstarterPackage -Package http://path/to/partial  
```

<p>this approach may works just like the web web call <a href="http://boxstarter.org/package/url?">http://boxstarter.org/package/url?</a> thingie, but unfortunately the packages are called the same, both are called temp_BoxStarterpackage and both have version 1.0. This causes the second install to go by quickly, as chocolatey already thinks the package is installed.</p>

<p>So my solution to this problem was to create chocolatey packages, so i took all my little powershell scripts, and packaged them up. Then i took my MSDN premium account and fired up a Nuget feed using Klondike on Azure.</p>

<p>This way i just need to have small powershell scripts that boxstarter will use, and then pull the packages from this private feed.</p>

<p>Just like this:  </p>

```posh
cinst domainjoin -source http://path/to/feed  
cinst notepadplusplus  
cinst procexp  
cinst baretail  
cinst fiddler4  
cinst updates -source http://path/to/feed  
```

<p>I could have pushed the need packages to my private feed and used that for all packages. But i don’t feel like maintaining every package might need that i did not make my self.</p>

<p>This is what i have done. If not only to remind my self what i did :)</p>
