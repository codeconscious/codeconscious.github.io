# Recursive Random Resource Renaming in Ruby

Certain files whose filenames contain Japanese characters cannot be copied from my Linux system to macOS. There's some character encoding conflict causing issues. (I haven't dug in too deeply yet, but that might be worth a post of its own once I do.)

In order to copy the files to my macOS device, I decided to give them random filenames. In this case, as long as the enclosed metadata was accessible, then the names were mostly superfluous.

Thinking it might be a good practice exercise, I created [a Ruby script](https://github.com/codeconscious/scripts/blob/main/ruby/recursive_random_rename.rb). Given a specified directory at the command line, it recursively and randomly renames all directories and either (1) all files or (2) only files of specified whitelisted extensions. File extensions are not changed.

Once run across my files, the files copied over without issue. The script scratched the itch pretty well. :-)
