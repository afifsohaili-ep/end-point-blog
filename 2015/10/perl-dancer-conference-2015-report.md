---
author: Josh Lavin
title: Perl Dancer Conference 2015 Report — Training Days
github_issue_number: 1167
tags:
- conference
- dancer
- interchange
- perl
date: 2015-10-28
---

I just returned from the [Perl Dancer Conference](https://www.perl.dance/), held in Vienna, Austria. It was a jam-packed schedule of two days of training and two conference days, with five of the nine Dancer core developers in attendance.

<div class="separator" style="clear: both; float:right; text-align: center;"><a href="/blog/2015/10/perl-dancer-conference-2015-report/image-0-big.jpeg" imageanchor="1" style="clear: right; float: right; margin-bottom: 1em; margin-left: 1em;" title="Vienna"><img alt="[image of Vienna]" border="0" src="/blog/2015/10/perl-dancer-conference-2015-report/image-0.jpeg"/></a><br/><br/><small>Kohlmarkt street, Wien, by this author</small></div>

If you aren’t familiar with [Perl Dancer](http://www.perldancer.org/), it is a modern framework for Perl for building web applications. Dancer1 originated as a port of Ruby’s Sinatra project, but has officially been replaced with a rewrite called Dancer2, based on [Moo](https://metacpan.org/pod/Moo), with Dancer1 being frozen and only receiving security fixes. The Interchange 5 e-commerce package is gradually being replaced by Dancer plugins.

**Day 1** began with a training on Dancer2 by [Sawyer X](https://twitter.com/PerlSawyer) and [Mickey Nasriachi](https://twitter.com/0xMickey), two Dancer core devs. During the training, the attendees worked on adding functionality to a [sample Dancer app](https://github.com/xsawyerx/dancer-training-vienna). Some of my takeaways from the training:

- Think of your app as a Dancer Web App *plus* an App. These should ideally be two separate things, where the Dancer web app provides the URL routes for interaction with your App.
- The lib directory contains all of your application. The recommendation for large productions is to separate your app into separate namespaces and classes. Some folks use a routes directory just for routing code, with lib reserved for the App itself.
- It is recommended to add an empty .dancer file to your app’s directory, which indicates that this is a Dancer app (other Perl frameworks do similarly).
- When running your Dancer app in development, you can use plackup -R lib bin/app.psgi which will restart the app automatically whenever something changes in lib.
- Dancer handles all the standard HTTP verbs, except note that we must use del, not *delete*, as *delete* conflicts with the Perl keyword.
- There are new keywords for retrieving parameters in your routes. Whereas before we only had param or params, it is now recommended to use:
    - route_parameters,
    - query_parameters, or
    - body_parameters
    - all of which can be used with ->get('foo') which is always a single scalar, or ->get_all('foo') which is always a list.
    - These allow you to specify which area you want to retrieve parameters from, instead of being unsure which param you are getting, if identical names are used in multiple areas.
   

**Day 2** was [DBIx::Class](https://metacpan.org/pod/DBIx::Class) training, led by [Stefan Hornburg](https://twitter.com/PerlRacke) and Peter Mottram, with assistance from [Peter Rabbitson](https://twitter.com/ribasushi), the DBIx::Class maintainer.

DBIx::Class (a.k.a. DBIC) is an [Object Relational Mapper](https://en.wikipedia.org/wiki/Object-relational_mapping) for Perl. It exists to provide a standard, object-oriented way to deal with SQL queries. I am new to DBIC, and it was a lot to take in, but at least one advantage I could see was helping a project be able to change database back-ends, without having to rewrite code (cue PostgreSQL vs MySQL arguments).

I took copious notes, but it seems that the true learning takes place only as one begins to implement and experiment. Without going into too much detail, some of my notes included:

 
- Existing projects can use dbicdump to quickly get a DBIC schema from an existing database, which can be modified afterwards. For a new project, it is recommended to write the schema first.
- DBIC allows you to place business logic in your application (not your web application), so it is easier to test (once again, the recurring theme of *Web App + App*).
- The *ResultSet* is a representation of a query before it happens. On any ResultSet you can call ->as_query to find the actual SQL that is to be executed.
- [DBIx::Class::Schema::Config](http://p3rl.org/DBIx::Class::Schema::Config) provides credential management for DBIC, and allows you to move your DSN/username/password out of your code, which is especially helpful if you use Git or a public GitHub.
- DBIC is all about relationships (belongs_to, has_many, might_have, and has_one). many_to_many is not a relationship per se but a convenience.
- [DBIx::Class::Candy](http://p3rl.org/DBIx::Class::Candy) provides prettier, more modern metadata, but cannot currently be generated by dbicdump.
- For deployment or migration, two helpful tools are [Sqitch](http://sqitch.org/) and [DBIx::Class::DeploymentHandler](http://p3rl.org/DBIx::Class::DeploymentHandler). Sqitch is better for raw SQL, while DeploymentHandler is for DBIC-managed databases. These provide easy ways to migrate, deploy, upgrade, or downgrade a database.
- Finally, [RapidApp](http://www.rapidapp.info/) can read a database file or DBIC schema and provide a nice web interface for interacting with a database. As long as you define your columns properly, RapidApp can generate image fields, rich-text editors, date-pickers, etc.

The training days were truly like drinking from a firehose, with so much good information. I am looking forward to putting this into practice!

Stay tuned for my [next blog post](/blog/2015/10/perl-dancer-conference-2015-report_30) on the Conference Days.
