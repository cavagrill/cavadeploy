# cavadeploy - standardized Python product deployments

The `cavadeploy` role deploys Cava Python products in a standard way.
Take a look at `example.yml` for an example of how to use it.
Variables that need to be set are:

- `product`: the name of the product, same as its repo name on GitHub
- `user`: the user to run this product, could be different than `product` or the same
- `do_cron`: whether or not to install cron jobs
- `cron_jobs`: a list of cron jobs, each with the following parameters
  - `name`: a unique name for the cron job
  - `day`, `hour`, `minute`, `month`, `weekday`: per the crontab(5) format
  - `job`: the command to run
  - `state`: `present` to create the job, `absent` to remove it
- `notify_slack`: whether or not to send a Slack notification
- `npm_install`: path in which to run `npm install`, or False if not needed
- `python_version`: either 2 or 3
- `slack_email`: email address for Slack email integration
- `slack_token`: token for Slack notifications

Defaults are:

- `cron_jobs`: empty list
- `do_cron`: True
- `notify_slack`: True
- `npm_install`: False
- `python_version`: 2

When using Python 2, a virtual environment will be created with
[virtualenv][venv2]. When using Python 2, it will be created with
[venv][venv3].

[venv2]: https://virtualenv.pypa.io/en/stable/
[venv3]: https://docs.python.org/3/library/venv.html

Note that we no longer use Conda as of October 9, 2017.

## Post script

If an executable file `cavadeploy_post.sh` exists at the root of the
repository being deployed, it will be executed as the final step of
deployment. Note that it will be executed on the _deployment host_,
**not** on the host where you are running ansible.
