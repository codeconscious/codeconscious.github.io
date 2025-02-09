# Installing Ruby on Rails on M1 MacBook Pro

I was surprised how much trouble I had installing Ruby on my M1 MacBook Pro. It was an astonishingly onerous and frustrating experience. I never had any significant problem installing .NET, Rust, Go, or any other language or framework I've worked with, but installing the latest versions of Ruby and Rails really took some doing.

(Perhaps the most egregious error was getting one telling me to run `sudo gem install rails` though multiple online sources state that you should definitely _not ever_ run this command in macOS due to risk of it borking some parts of your installation or system.)

However, after many twists and turns, I finally discovered the apparent cause of the problems: I'd originally migrated all my applications and data from my old Intel MacBook to my M1 one (using Time Machine, as I recall). However, Homebrew is expected to be installed in different directories in the differing architectures — specifically, `/usr/local/` in x86 and `/opt/homebrew/` in arm64.

I ultimately took a risk and reinstalled Homebrew from scratch to its proper arm64 directory (after backing up my system, of course), and that seems to have resolved the issue as I was able to successfully install Ruby on Rails after that. (I think some applications or casks installed via Homebrew might not have been successfully relinked to the new installation yet, but nothing has caused any trouble yet.)

These were the main pages that helped me confirm the issue and succesfully install Ruby on Rails: 
- StackOverflow: [mac os ruby installation fails on -> make -j 8](https://stackoverflow.com/questions/78064794/mac-os-ruby-installation-fails-on-make-j-8)
- StackOverflow: [Apple Silicon M1 Chip - Homebrew installer installing into Intel folder](https://apple.stackexchange.com/questions/435135/apple-silicon-m1-chip-homebrew-installer-installing-into-intel-folder)
- Blog: "[Install native arm64 Ruby through rbenv on Apple Silicon](https://posts.boy.sh/install-ruby-on-apple-silicon)"

I hope this helps someone in the future.
