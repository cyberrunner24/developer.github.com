---
title: Repo Contents | GitHub API
---

# Repo Contents API

These API methods let you retrieve the contents of files within a repository as
Base64 encoded content. See [Mime types](http://localhost:3002/v3/mime/) for requesting raw or other formats.

## Get the README

This method returns the preferred README for a repository.

    GET /repos/:user/:repo/readme

### Response

<%= headers 200 %>
<%= json :readme_content %>

## Get contents

This method returns the contents of any file or directory in a repository.

    GET /repos/:user/:repo/contents/:path

### Response

<%= headers 200 %>
<%= json :readme_content %>

## Get archive link

This method will return a `302` to a URL to download a tarball
or zipball archive for a repository. Please make sure your HTTP framework
is configured to follow redirects or you will need to use the `Location` header
to make a second `GET` request.

*Note*: For private repositories, these links are temporary and expire quickly.

    GET /repos/:user/:repo/:archive_format/:ref

### Parameters

archive_format
: Either `tarball` or `zipball`

ref (optional)
: _Optional_ valid Git reference, defaults to `master`

### Response

<%= headers 302, :Location => 'http://github.com/me/myprivate/tarball/master?SSO=thistokenexpires' %>

To follow redirects with curl, use the `-L` switch:

<pre class="terminal">
curl -L https://api.github.com/repos/pengwynn/octokit/tarball > octokit.tar.gz

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  206k  100  206k    0     0   146k      0  0:00:01  0:00:01 --:--:--  790k
</pre>