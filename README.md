<p align="center">
    <h1 align="center">Mr KayZ's Extra Notes</h1>
    <p align="center">A Personal Extension to the r/techsupport Wiki</p>
    <br>
</p>

## Purpose of this Wiki

Hello! This is a personal extension of the [r/techsupport wiki](https://rtech.support/) that explores more obscure and unknown tech issues and provides unique fixes beyond standard troubleshooting methods.

This wiki serves as a resource for solving rare and perplexing technical problems with innovative solutions. (Also because I can update this faster than the official r/techsupport wiki lol.)

It also serves as a personal notes collection of which that allows me to quickly refer to issues and topics I would need further reading on (especially if not documented in the Wiki at the time of writing).

## How can I contribute?

If you wish to see more articles and potential fixes, feel free to reach out to me using the email [mrkayz.wiki@gmail.com](mailto:mrkayz.wiki@gmail.com) to give me tips on other current tech issues that require a unique way to solve them. I would gladly appreciate any information I can get!

If you have tech issues, please feel free to write up the issue in the reddit [TechSupport (reddit.com)](https://www.reddit.com/r/techsupport/). Otherwise, you can head to the live chat [Discord](https://discord.com/invite/2EDwzWa) to chat with helpers, including me!

## Setting up repo and running it locally:
Refer to https://github.com/just-the-docs/just-the-docs/blob/main/README.md for more information. Summary is as follows:

- Ensure you have the following installed:
    - Ruby - https://www.ruby-lang.org/en/downloads/
        - Check Ruby version by running `ruby -v`.
    - RubyGems - https://rubygems.org/pages/download
        - Check Gems version by running `gem -v`
    - GCC and Make (obsolete?) - https://gcc.gnu.org/install/ and https://www.gnu.org/software/make/
        - Check versions using `gcc -v`,`g++ -v`, and `make -v`.
- Ensure that dependancies are installed via running `bundle install` from root directory.
- Run the site by running `bundle exec jekyll serve` from root directory.