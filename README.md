# localdev-envs

Repository for creating vagrant based localdev setups for various different language stacks by adding this repo as a git submodule and then checking out the relevant branch.

Look at the branches to see the list of development stacks supported.

Branch naming convention: <vagrant provider>-<language stack> e.g. docker-python for a docker based python development environment.

These aren't seperated into their own repos because they won't besetup with CI so we can get the benefit of a centralized repo.

## usage

Clone the this repo into yor project with the following command

```
git submodule add https://github.com/mtbvang/localdev-envs localdev
```

Then checkout the desired branch and vagrant up to spin up the devlopment environment. 

```
cd localdev
git checkout docker-python
vagrant up
vagrant ssh
```.

