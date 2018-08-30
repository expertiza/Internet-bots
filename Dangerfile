# ------------------------------------------------------------------------------
# Has any changes happened inside the actual library code?
# ------------------------------------------------------------------------------
if github.pr_author
  WELCOME_MESSAGE = 
    markdown <<-MARKDOWN
Thanks for the pull request, and welcome! :tada: The Expertiza team is excited to review your changes, and you should hear from us soon.

This repository is being automatically checked for code quality issues using `Code Climate`. You can see results for this analysis in the PR status below. Newly introduced issues should be fixed before a Pull Request is considered ready to review.

If you have any questions, please send email to <a href="mailto:expertiza-support@lists.ncsu.edu">expertiza-support@lists.ncsu.edu</a>.
    MARKDOWN

  message(WELCOME_MESSAGE, sticky: true) 
end

# ------------------------------------------------------------------------------
# You've made changes to lib, but didn't write any tests?
# ------------------------------------------------------------------------------
has_app_changes = !git.modified_files.grep(/app/).empty?
has_spec_changes = !git.modified_files.grep(/spec/).empty?

if has_app_changes && !has_spec_changes
  if Dir.exist?('spec')
    NO_TEST_MESSAGE = 
      markdown <<-MARKDOWN
There are code changes, but no corresponding tests.
Please include tests if this PR introduces any modifications in behavior.
      MARKDOWN

    warn(NO_TEST_MESSAGE, sticky: true)
  else
    markdown <<-MARKDOWN
Thanks for the PR! This project lacks automated tests, which makes reviewing and approving PRs somewhat difficult.
Please make sure that your contribution has not broken backwards compatibility or introduced any risky changes.
    MARKDOWN
  end
end

# ------------------------------------------------------------------------------
# Your pull request is too big (more than 500 LoC)
# ------------------------------------------------------------------------------
if git.lines_of_code > 500
  BIG_PR_MESSAGE = 
    markdown <<-MARKDOWN
Your pull request is more than 500 LoC.
Please make sure you did not commit unnecessary changes, such as `node_modules`, `change logs`.
    MARKDOWN

  warn(BIG_PR_MESSAGE, sticky: true)
end

# ------------------------------------------------------------------------------
# If a PR is a work in progress and it shouldn't be merged
# ------------------------------------------------------------------------------
if github.pr_title.include? "WIP" or github.pr_title.include? "wip"
  warn("This pull request is classed as Work in Progress", sticky: true)
end





