---
layout: post
title: "Fun with GIT and AWK"
date: 2014-06-11 21:53:43 -0500
comments: true
categories: 
---
For those of you who use GIT, you have probably noticed that while it is an incredibly powerful tool, one area that it
could use some help is reporting.  For example, Let's say that I want to determine all changes to a file provided a date
range... how would you do that?  While there are many plugin utilities out there that provide reporting to GIT, very
rarely will you find a utility that is able to generate the report you need at all times.

One thing that many people do not realize is that within GIT you can easily pipe the log to another application and
quite literally build your won reports from within the command line.  One of the more powerful applications that you
can utilize is AWK, which allows you to write some code that parses through a log to generate a report to your needs.

Here are a few that I created to give you an idea of what you can do with this technique.
<!-- more -->

  __Determine how productive your team has been using git history.__
{% codeblock lang:bash %}
git log --shortstat --since="1 year ago" --until="now" \
  | grep "files changed\|Author\|Merge:" \
  | awk '{ \
    if ($1 == "Author:") {\
      currentUser = $2;\
    }\
    if ($2 == "files") {\
      files[currentUser]+=$1;\
      inserted[currentUser]+=$4;\
      deleted[currentUser]+=$6;\
    }\
  } END {\
    for (i in files) {\
      print i ":", "files changed:", files[i], "lines inserted:", inserted[i], "lines deleted:", deleted[i];\
    }\
  }'
{% endcodeblock %}

  __Determine all changes to a file provided a date range in GIT.__
{% codeblock lang:bash %}
git log --shortstat --since="3 weeks ago" --until="now" \
  | grep "Merge pull request" -B 5\
  | awk '{\
    if ($1=="commit") {\
      output = system("git diff " $2 "^ " $2 " {YOUR FILE HERE}");\
      if (output) {\
        print output;\
      }\
    }\
  }'
{% endcodeblock %}

  __Determine the diff provided a Pivotal Tracker Story ID.__

{% codeblock lang:bash %}
git log\
  | grep "Merge pull request.*{INSERT STORY ID HERE}" -B 5\
  | awk '{\
    if ($1=="commit") {\
      print system("git diff " $2 "^ " $2);\
    }\
  }'
{% endcodeblock %}

  __Determine all commits for a developer given a time range.__

{% codeblock lang:bash %}
git log --shortstat --since="2011-9-1" --until="2011-11-15" \
  | grep "commit\|Author\|Merge:" \
  | awk '{\
    if ($1 == "Merge:") {\
      merge = 1;\
    }\
    if ($1 == "commit") {\
      merge = 0;\
      commit = $2;\
    }\
    if ($1 == "Author:" && tolower($2) == tolower("Travis")) {\
      if (!merge) {\
        merge = 0;\
        print system("git diff " commit "^ " commit);\
      }\
    }\
  }'
{% endcodeblock %}

I hope everyone finds this useful.  Now use the comments to share your own GIT with AWK magic!
