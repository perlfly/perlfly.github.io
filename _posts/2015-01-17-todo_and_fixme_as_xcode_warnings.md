---
layout: post
title: "//TODO: and //FIXME: as XCode Warnings"
description: "Formula Update"
tags: [xcode]
---

`//TODO:` and `//FIXME:` can be turned in warnings during the build phase adding a 
_Run Script Phase_ to your target's _Build Phases_ tab.

Then add this shell script code:

{% highlight bash %}	
TAGS="\/\/TODO:|\/\/FIXME:"
echo "searching ${SRCROOT} for ${TAGS}"
find "${SRCROOT}" \( -name "*.swift" \) -print0 | xargs -0 egrep --with-filename --line-number --only-matching "^\s*($TAGS).*\$" | perl -p -e "s/($TAGS)/ warning: \$1/"
{% endhighlight %}	
	
The code above is a minor improvement of the solution proposed by [Ben Dodson]. It will trigger the warning only if the line starts
with white spaces.


[Ben Dodson]: http://bendodson.com/weblog/2014/10/02/showing-todo-as-warning-in-swift-xcode-project/


	