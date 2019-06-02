# localdev-envs

Repository for creating vagrant based localdev setups for various different language stacks by adding this repo as a git submodule and then checking out the relevant branch.

Look at the branches to see the list of development stacks supported.

Branch naming convention: <vagrant provider>-<language stack> e.g. docker-python for a docker based python development environment.

These aren't seperated into their own repos because they won't besetup with CI so we can get the benefit of a centralized repo.

## Configuring git in the guest

Commands to configure git in the guest.

```
git config --global credential.helper store
git config --global user.name "<REPLACE WITH USERNAME>"
git config --global user.email <REPLACE WITH EMAIL>
```