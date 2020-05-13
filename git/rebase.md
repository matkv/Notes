# Git Rebase

Let's say we have a `develop` branch and then merge it with `master`. Now `master` has one additional commit and `develop` is "1 commit behind master".

We can fix this by checking out the `develop` branch - `git checkout develop` and the running the command:

 `git rebase master`

Now we just need to push again & the `develop` branch will get this one additional commit and won't be behind `master` anymore.