---
layout: post
title: Remove Old AWS Elastic Beanstalk Application Versions (Bash & Cron Edition)
---

We ran into the [TooManyApplicationVersions](http://docs.aws.amazon.com/elasticbeanstalk/latest/api/API_CreateApplicationVersion.html) Exception and our developers got quickly annoyed clicking checkboxes in the AWS console to delete versions. Inspired by [Dan Mandles](http://www.danmandle.com/blog/automatically-remove-old-aws-elastic-beanstalk-application-versions/) post using PHP I wrote a shell script using the AWS CLI and scheduling it through a cronjob. It requires a configured [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html). 

Usage example:
{% highlight bash %}
# Keep the last 40 versions of app 'foo-app' and delete all beyond
$ ./purgeAppVersions.sh foo-app 40
Tue Feb  3 15:51:18 UTC 2015    checking app:foo-app with limit:40
Tue Feb  3 15:51:24 UTC 2015    foo-app:build-2015-01-29_16-48-35#178-dev deleted
Tue Feb  3 15:51:28 UTC 2015    foo-app:build-2015-01-29_16-38-45#177-dev deleted
Tue Feb  3 15:51:31 UTC 2015    foo-app:build-2015-01-29_16-28-58#176-dev deleted
{% endhighlight %}

The actual script:

{% highlight bash %}
#!/bin/bash
# 08.01.2015 Frank
# Delete obsolete elasticbeanstalk app versions
#
PATH=/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/opt/aws/bin:/home/ec2-user/bin

# set defaults for name and limit
_appName=${1:-foo-app}
_limit=${2:-"45"}

echo "$(date)    checking app:$_appName with limit:$_limit "

# get app versions above the limit as a list
versions=$(aws elasticbeanstalk describe-application-versions\
    --application-name $_appName\ 
    --query ApplicationVersions[*].[VersionLabel]\
    --output text | tail -n +$_limit)

# delete obsolete versions
for version in $versions
do
    aws elasticbeanstalk delete-application-version --delete-source-bundle\
        --version-label "$version" --application-name "$_appName"
    echo "$(date)    $_appName:$version deleted"
done
{% endhighlight %}

Scheduling the script hourly as a cronjob:

{% highlight bash %}
# Delete obsolete application versions
@hourly /home/ec2-user/purgeAppVersions.sh foo-app 45 >> /home/ec2-user/purgeAppVersions.log
{% endhighlight %}

Told my developers they never have to delete versions manually again and enjoyed being celebrated as the king of devops ;)


