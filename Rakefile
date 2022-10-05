desc "Check git status"
task :check do
  puts "\n## Checking that current branch is 'source'"
  status = system('[ "$(git branch --show-current)" = "source" ]')
  status ? puts("SUCCESS") : abort("`rake` commands must be run from the 'source' branch!`")
  puts "\n## Checking that working copy is up-to-date with remote"
  status = system(
    "[ $(git rev-parse HEAD) = $(git ls-remote $(git rev-parse --abbrev-ref @{u} | sed 's|/| |g') | cut -f1) ]")
  status ? puts("SUCCESS") :
           abort("Your working copy (local) is not up-to-date with remote; `git pull` and merge as necessary")
end

desc "Build _site/ for production"
task :build do
  puts "\n## Building Jekyll to _site/"
  status = system("JEKYLL_ENV=production bundle exec jekyll build")
  status ? puts("SUCCESS") : abort("FAILED")
end

desc "Preview _site/ for production"
task :preview do
  puts "\n## Previewing Jekyll to _site/"
  status = system("JEKYLL_ENV=production bundle exec jekyll serve")
  status ? puts("SUCCESS") : abort("FAILED")
end

desc "Commit and deploy _site/"
task :publish => [:check, :build] do
end
