# Hosting Service URL Pattern and API Reference #

The URLs of Hosting services such as GitHub, GitLab and Bitbucket have
their patterns.  Thus we can use these patterns to compose the URL of
a file or the repo on a specific commit rather than clicking several
links in a row to get to where we want.  They also provide their own
APIs for doing that, which sometimes are more intuitive to use.

Below is a collection of the patterns and APIs that are used in
[MLHub](https://mlhub.ai/) to construct the URLs for MLHub package
installation from these hosting services.


## GitHub ##

### Web URL ###

* Repo webpage:
  - https://github.com/:owner/:repo (Default)
  - https://github.com/:owner/:repo/tree/:branch (Branch)
  - https://github.com/:owner/:repo/tree/:sha (Commit)
* File webpage:
  - https://github.com/:owner/:repo/blob/master/:path (Default)
  - https://github.com/:owner/:repo/blob/:branch/:path (Branch)
  - https://github.com/:owner/:repo/blob/:sha/:path (Commit)
* Raw file:
  - https://raw.githubusercontent.com/:owner/:repo/master/:path (Default)
  - https://raw.githubusercontent.com/:owner/:repo/:branch/:path (Branch)
  - https://raw.githubusercontent.com/:owner/:repo/:sha/:path (Commit)
* Directory:
  - https://github.com/:owner/:repo/tree/master/:path (Default)
  - https://github.com/:owner/:repo/tree/:branch/:path (Branch)
  - https://github.com/:owner/:repo/tree/:sha/:path (Commit)
* Commit:
  - https://github.com/:owner/:repo/commit/:sha (From commit list)
* Repo zip:
  - https://github.com/:owner/:repo/archive/master.zip (Default)
  - https://github.com/:owner/:repo/archive/:branch.zip (Branch)
  - https://github.com/:owner/:repo/archive/:sha.zip (Commit)
* Git clone:
  - https://github.com/:owner/:repo.git
* Tag:
  - https://github.com/:owner/:repo/tree/:tag (Webpage)
  - https://github.com/:owner/:repo/blob/:tag/:path (File webpage)
  - https://github.com/:owner/:repo/raw/:tag/:path (Raw file)
  - https://github.com/:owner/:repo/tree/:tag/:path (Directory)
* Release:
  - https://github.com/:owner/:repo/releases/tag/:release
* Pull request:
  - https://github.com/:owner/:repo/pull/:number (From pull request list)
  - https://github.com/:owner/:repo/pull/:number/commits (Pull request commits)
  - https://github.com/:owner/:repo/pull/:number/commits/:sha (A single commit in pull request)

### API URL ###

* File:
  + https://api.github.com/repos/:owner/:repo/contents/:path
    - Reponse contains the `type` of the path (file or dir),
      `name`, encoded `content` of the file and
      `download_url`.
* Directory:
  + https://api.github.com/repos/:owner/:repo/contents/:path
    - Response is an array of JSON objects which contains the
      `type` of the object (file or dir), `name`,
      encoded `content` of the file (if it is file) and
      `download_url` (if it is a file).
* Repo zip:
  + https://api.github.com/repos/:owner/:repo/zipball/:ref
    - Response contains `location` of the redirected link of
      the repo's zipball referred by `:ref` which may be a
      commit, tag, release or branch, I think.
* Pull request commits list:
  + https://api.github.com/repos/:owner/:repo/pulls/:pull_number/commits


## GitLab ##

### Web URL ###

* Repo webpage:
  - https://gitlab.com/:owner/:repo (Default)
  - https://gitlab.com/:owner/:repo/tree/:branch (Branch)
  - https://gitlab.com/:owner/:repo/tree/:sha (Commit)
* File webpage:
  - https://gitlab.com/:owner/:repo/blob/master/:path (Default)
  - https://gitlab.com/:owner/:repo/blob/:branch/:path (Branch)
  - https://gitlab.com/:owner/:repo/blob/:sha/:path (Commit)
* Raw file:
  - https://gitlab.com/:owner/:repo/raw/master/:path (Default)
  - https://gitlab.com/:owner/:repo/raw/master/:path?inline=false (Default download)
  - https://gitlab.com/:owner/:repo/raw/:branch/:path (Branch)
  - https://gitlab.com/:owner/:repo/raw/:branch/:path?inline=false (Branch download)
  - https://gitlab.com/:owner/:repo/raw/:sha/:path (Commit)
  - https://gitlab.com/:owner/:repo/raw/:sha/:path?inline=false (Commit download)
* Directory:
  - https://gitlab.com/:owner/:repo/tree/master/:path (Default)
  - https://gitlab.com/:owner/:repo/tree/:branch/:path (Branch)
  - https://gitlab.com/:owner/:repo/tree/:sha/:path (Commit)
* Commit:
  - https://gitlab.com/:owner/:repo/commit/:sha (From commit list)
* Repo zip:
  - https://gitlab.com/:owner/:repo/-/archive/master/:repo-master.zip (Default)
  - https://gitlab.com/:owner/:repo/-/archive/:branch/:repo-:branch.zip (Branch)
  - https://gitlab.com/:owner/:repo/-/archive/:sha/:repo-:sha.zip (Commit)
* Git clone:
  - https://gitlab.com/:owner/:repo.git
* Tag:
  - https://gitlab.com/:owner/:repo/tree/:tag (Webpage)
  - https://gitlab.com/:owner/:repo/blob/:tag/:path (File webpage)
  - https://gitlab.com/:owner/:repo/raw/:tag/:path (Raw file)
  - https://gitlab.com/:owner/:repo/raw/:tag/:path?inline=false (Raw file download)
  - https://gitlab.com/:owner/:repo/tree/:tag/:path (Directory)
* Release: Created by API, not directly in webpage.  And a release
  seems to be referred by the tag it relies on not its release name.
  - https://gitlab.com/:owner/:repo/-/archive/:tag/:repo-:tag.zip (Download)
* Merge request:
  - https://gitlab.com/:owner/:repo/merge_requests/:number (From merge request list)
  - https://gitlab.com/:owner/:repo/merge_requests/:number/commits (Merge request commits)
  - https://gitlab.com/:owner/:repo/merge_requests/:number/diffs?commit_id=:sha (A single commit in merge request)

### API URL ###

* File info:
  + https://gitlab.com/api/v4/projects/:id/repository/files/:path?ref=:ref}
    - Response contains the `size` of the file, enconded `content`.
      Note: `:id` is `:owner/:repo` but needs to be encoded as
      `:owner%2F:repo`, where `/` is replaced by `%2`.  Similarly,
      `:path` such as `mlhub/commands.py` needs to be encoded as
      `mlhub%2Fcommands%2Epy`.  `:ref` can be a branch, commit, tag,
      etc.
* Raw file:
  + https://gitlab.com/api/v4/projects/:id/repository/files/:path/raw?ref=:ref}
* Directory:
  + https://gitlab.com/api/v4/projects/:id/repository/tree?path=:path&ref=:ref}
    - Response is an array of JSON objects which contains the
      `type` of the object (blob or tree) and `name` of
      the file or directory.
* Repo zip:
  + https://gitlab.com/api/v4//projects/:id/repository/archive.zip?sha=:ref}
* Merge request commits list:
  + https://gitlab.com/api/v4/projects/:id/merge_requests/:merge_request_iid/commits}


## BitBucket ##

### Web URL ###

* Repo webpage:
  - https://bitbucket.org/:owner/:repo/src/master/ (Default source)
  - https://bitbucket.org/:owner/:repo/src/:branch/ (Branch source)
  - https://bitbucket.org/:owner/:repo/branch/:branch (Branch)
  - https://bitbucket.org/:owner/:repo/src/:sha/ (Commit source)
  - https://bitbucket.org/:owner/:repo/commits/:sha (Commit)
  - https://bitbucket.org/:owner/:repo/commits/:sha?at=:branch (Commit on a branch)
* File webpage:
  - https://bitbucket.org/:owner/:repo/src/master/:path (Default)
  - https://bitbucket.org/:owner/:repo/src/:branch/:path (Branch)
  - https://bitbucket.org/:owner/:repo/src/:sha/:path (Commit)
* Raw file:
  - https://bitbucket.org/:owner/:repo/raw/master/:path (Default)
  - https://bitbucket.org/:owner/:repo/raw/:branch/:path (Branch)
  - https://bitbucket.org/:owner/:repo/raw/:sha/:path (Commit)
* Directory:
  - https://bitbucket.org/:owner/:repo/src/master/:path/ (Default)
  - https://bitbucket.org/:owner/:repo/src/:branch/:path/ (Branch)
  - https://bitbucket.org/:owner/:repo/src/:sha/:path/ (Commit)
* Commit:
  - https://bitbucket.org/:owner/:repo/commits/:sha (From commit list)
* Repo zip:
  - https://bitbucket.org/:owner/:repo/get/master.zip (Master)
  - https://bitbucket.org/:owner/:repo/get/:branch.zip (Branch)
  - https://bitbucket.org/:owner/:repo/get/:sha.zip (Commit)
* Git clone:
  - https://bitbucket.org/:owner/:repo.git
* Tag:
  - https://bitbucket.org/:owner/:repo/src/:tag/ (Webpage)
  - https://bitbucket.org/:owner/:repo/src/:tag/:path (File webpage)
  - https://bitbucket.org/:owner/:repo/raw/:tag/:path (Raw file)
  - https://bitbucket.org/:owner/:repo/src/:tag/:path/ (Directory)
* Release: There seems no release.  But there are downloads which
  seems to be any files not only repo archives.
* Pull request:
  - https://bitbucket.org/:owner/:repo/pull-requests/:number (From pull request list)
  - https://bitbucket.org/:owner/:repo/pull-requests/:number/:branch/diff (Redirection from above)
  - https://bitbucket.org/:owner/:repo/pull-requests/:number/:branch/commits (Pull request commits)
  - https://bitbucket.org/:owner/:repo/commits/:sha?at=:branch (A
    single commit in pull request): It rolls back to a plain commit.
    So the SHA of the commit needs to be known beforehand.

### API URL ###

* File:
  + https://api.bitbucket.org/2.0/repositories/:owner/:repo/src/:ref/:path
* Directory: The same as file.
* Repo zip: There seems no relevant API.
* Pull request: There seems no relevant API.


## Reference ##

* GitHub REST API v3
  - [Response if content is a file -- Contents](https://developer.github.com/v3/repos/contents/#response-if-content-is-a-file)
  - [Response if content is a directory -- Contents](https://developer.github.com/v3/repos/contents/#response-if-content-is-a-directory)
  - [Get archive link -- Contents](https://developer.github.com/v3/repos/contents/#get-archive-link)
  - [List commits on a pull request -- Pull Requests](https://developer.github.com/v3/pulls/#list-commits-on-a-pull-request)
  
* GitLab REST API v4
  - [Get file from repository -- Repository files API](https://docs.gitlab.com/ee/api/repository_files.html#get-file-from-repository)
  - [Get raw file from repository -- Repository files API](https://docs.gitlab.com/ee/api/repository_files.html#get-raw-file-from-repository)
  - [List repository tree -- Repositories API](https://docs.gitlab.com/ee/api/repositories.html#list-repository-tree)
  - [Get file archive -- Repository files API](https://docs.gitlab.com/ee/api/repositories.html#get-file-archive)
  - [Get single MR commits -- Merge requests API](https://docs.gitlab.com/ee/api/merge_requests.html#get-single-mr-commits)
  
* BitBucket REST API v2
  - [Path -- Repositories](https://docs.gitlab.com/ee/api/merge_requests.html#get-single-mr-commits)
