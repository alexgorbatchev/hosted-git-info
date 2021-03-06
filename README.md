# hosted-git-info

This will let you identify and transform various git hosts URLs between
protocols.  It also can tell you what the URL is for the raw path for
particular file for direct access without git.

## Usage

```javascript
var hostedGitInfo = require("hosted-git-info")
var info = hostedGitInfo("git@github.com:npm/hosted-git-info.git")
/* info looks like:
{
  type: "github",
  domain: "github.com",
  user: "npm",
  project: "hosted-git-info"
}
*/
```

If the URL can't be matched with a git host, `null` will be returned.  We
can match git, ssh and https urls.  Additionally, we can match ssh connect
strings (`git@github.com:npm/hosted-git-info`) and shortcuts (eg,
`github:npm/hosted-git-info`).  Github specifically, is detected in the case
of a third, unprefixed, form: `npm/hosted-git-info`.

If it does match, the returned object has properties of:

* info.type -- The short name of the service
* info.domain -- The domain for git protocol use
* info.user -- The name of the user/org on the git host
* info.project -- The name of the project on the git host

And methods of:

* info.file(path)

Given the path of a file relative to the repository, returns a URL for
directly fetching it from the githost.  If no comittish was set then
`master` will be used as the default.

For example `hostedGitInfo("git@github.com:npm/hosted-git-info.git").file("v1.0.0")`
would return `https://raw.githubusercontent.com/npm/hosted-git-info/v1.0.0/package.json`

* info.shortcut()

eg, `github:npm/hosted-git-info`

* info.browse()

eg, `https://github.com/npm/hosted-git-info/tree/v1.2.0`

* info.bugs()

eg, `https://github.com/npm/hosted-git-info/issues`

* info.docs()

eg, `https://github.com/npm/hosted-git-info/tree/v1.2.0#readme`

* info.https()

eg, `https://github.com/npm/hosted-git-info.git`

* info.sshurl()

eg, `git+ssh://git@github.com/npm/hosted-git-info.git`

* info.ssh()

eg, `git@github.com:npm/hosted-git-info.git`

* info.path()

eg, `npm/hosted-git-info`

## Supported hosts

Currently this supports Github, Bitbucket and Gitlab. Pull requests for
additional hosts welcome.

