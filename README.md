"build_num" : 23,
  "branch" : "master",
  "vcs_revision" : "1d231626ba1d2838e599c5c598d28e2306ad4e48",
  "committer_name" : "Allen Rohner",
  "committer_email" : "arohner@gmail.com",
  "subject" : "Don't explode when the system clock shifts backwards",
  "body" : "", // commit message body
  "why" : "retry", // short string explaining the reason we built
  "dont_build" : null, // reason why we didn't build, if we didn't build
  "queued_at" : "2013-04-12T21:33:30Z" // time build was queued
  "start_time" : "2013-04-12T21:33:38Z", // time build started running
  "stop_time" : "2013-04-12T21:34:01Z", // time build finished running
  "build_time_millis" : 23505,
  "lifecycle" : "queued",
  "outcome" : null,
  "status" : "queued",
  "retry_of" : 22, // build_num of the build this is a retry of
  "previous" : { // previous build
    "status" : "failed",
    "build_num" : 22
  }


#### [tests](#tests)

Endpoint: `/project/:username/:repository/:build/tests`

Tests endpoint to get the recorded tests for a build. Will return an array of
the tests ran and some details.


ruby
# Use global config with token for user
build = CircleCi::Build.new 'username', 'reponame', nil, 'build'
res = build.tests

# Use a different config with another user token
build = CircleCi::Build.new 'username', 'reponame', nil, 'build', other_build_config
build.tests



javascript
[
  {
    "message" => nil,
    "file" => "spec/unit/user_spec.rb",
    "source" => "rspec",
    "run_time" => 0.240912,
    "result" => "success",
    "name" => "user creation",
    "classname"=> "spec.unit.user_spec"
  },
  {
    "message" => "Unable to update user",
    "file" => "spec/unit/user_spec.rb",
    "source"=>"rspec",
    "run_time"=>5.58533,
    "result"=>"failure",
    "name"=>"user update",
    "classname"=>"spec.unit.user_spec"
  }
]


### [recent_builds](#recent_builds)

#### [get_recent_builds](#get_recent_builds)

Endpoint: `/recent-builds`

Build summary for each of the last 30 recent builds, ordered by build_num.


ruby
# Use global config with token for user
recent = CircleCi::RecentBuilds.new
res = recent.get

# Params of limit and offset can be passed in
res = recent.get limit: 10, offset: 50

# Use a different config with another user token
recent = CircleCi::RecentBuilds.new other_builds_config
recent.get



javascript
[ {
  "vcs_url" : "https://github.com/circleci/mongofinil",
  "build_url" : "https://circleci.com/gh/circleci/mongofinil/22",
  "build_num" : 22,
  "branch" : "master",
  "vcs_revision" : "1d231626ba1d2838e599c5c598d28e2306ad4e48",
  "committer_name" : "Allen Rohner",
  "committer_email" : "arohner@gmail.com",
  "subject" : "Don't explode when the system clock shifts backwards",
  "body" : "", // commit message body
  "why" : "github", // short string explaining the reason we built
  "dont_build" : null, // reason why we didn't build, if we didn't build
  "queued_at" : "2013-02-12T21:33:30Z" // time build was queued
  "start_time" : "2013-02-12T21:33:38Z", // time build started
  "stop_time" : "2013-02-12T21:34:01Z", // time build finished
  "build_time_millis" : 23505,
  "username" : "circleci",
  "reponame" : "mongofinil",
  "lifecycle" : "finished", // :queued, :scheduled, :not_run, :not_running, :running or :finished
  "outcome" : "failed", // :canceled, :infrastructure_fail, :timedout, :failed, :no_tests or :success
  "status" : "failed", // :retried, :canceled, :infrastructure_fail, :timedout, :not_run, :running, :failed, :queued, :scheduled, :not_running, :no_tests, :fixed, :success
  "retry_of" : null, // build_num of the build this is a retry of
  "previous" : { // previous build
    "status" : "failed",
    "build_num" : 21
  }, ... ]
`

### Tests

Tests are ran using Rspec and VCR for API interaction recording.
Run using `rake` or `rspec`. Please add tests for any new features or
endpoints added if you are contributing. Code styling is enforced with RuboCop
and uses a checked in `.rubocop.yml` for this project.

Tests are using a live CircleCi API token for this repository. Any tests
should be using this key, which is in the .env file. You should not have
to do anything outside of writing the tests against this repository.


[docs]: http://www.rubydoc.info/gems/circleci
