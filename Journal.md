## 2017 11 28, Tuesday

This is my last week at @Flipkart! Thursday- November 30th will be my last day
of work, after which I go on a 4-month sabbatical. I have to return all my IT
assets. Bye bye MacBook Pro :'-(

TODOs for this week:

1. Write a blog post about Outreachy selection and/or a project description. Writing one every two weeks is one of the mandatory parts of the internship. I did set up a blog last week using hugo at aishpant.github.io but it's empty.

2. Back up data from office laptop.

3. Set up the borrowed laptop with the linux codebase and all my dotfiles.

4. Become friends with tmux.

5. Go through the vimtutor tutorial 3 more times.

## 2017 11 29, Wednesday

Finished one iteration of the vimtutor tutorial. Added first proper blog post on
my blog! It's kind of temporary and rough but it's finally a start! With this
done, I sent off the links to Outreachy organisers.

Cleaned up the deployment of personal website. Added aishpant.github.io as a
submodule to hugo content repo. Didn't know that tracking of two different repos
was possible in this way.

Currently working through a Markdown tutorial. I want to get this right. Should
add social links to the blog site.

The hard drive was delivered today. Backed up all office data. The other
important stuff is tracked already. Not much left to do here. Things move
forward very slowly. Reviewed a pull request.

Oh that reminds me I should backup dotfiles from my VM also. I'll do that.

## 2017 11 30, Thursday

Last day of work. Feeling odd. Mixed feelings. Went out in the evening.

## 2017 12 01, Friday

Spent most of the day struggling with Arch Linux. I fail to see how this is any
better than Ubuntu or Debian or Mint or Fedora.

`pacman` is the default PACkage MANager here. The tldr page is enough to get
started. The other, `yaourt` works just like pacman and contains scripts to
download the lastest packages that have not made into official repos yet.

I should do a newbie write-up on how to compile linux kernel in arch.

## 2017 12 04, Monday

Doesn't really feel like a Monday. Cold weather (for Bangalore) and lazy.
Needed one chai and two cups of coffee to wake up.

TIL about the PBKDF2 (Password Based Key Derivation Function v2). Maybe I could
talk about this at a PWL. My day job has never involved reading white papers.
And if I don't read any, I'm afraid I might become out-of-date. Another aspect
of this which interests me is speaking in public. I don't think I have ever
done it out of choice. I have reached a point now where it is necessary to
embrace fear.

Read lots of blog posts by Jeffrey Goldberg (Defender Against The Dark Arts at
1Password). In each iteration, password or the transformed key is encrypted by
a process called HMAC-SHA1(?).

Password hashing algorithms are designed to be purposefully slow in contrast to
crypotgraphic hashing functions. Some good password hashing schemes:
1. bcrypt
2. scrypt
3. PBKDF2

Usually salting is added before passwords are encrypted. For eg. adding a
random string at the beginning or the end. This is done to prevent check
against a pre-computed list of hashes. The salt is not a secret. It's random
and uniquely generated per password.

Today I also learnt how 2-step authentication works using HOTP or TOTP
protocols! I am already on GNU pass but I still had a couple of old weak
passwords. It was a pain trying to figure out how to enable copy-paste on ICICI
bank website. You wouldn't expect bank websites to be clueless about security.

Read 2 chapters of I,Robot. This is my first Asimov. Why did I not read him
before?

[Giorgio by Morodor - Daft Punk](https://youtu.be/zhl-Cs1-sG4) - Beautiful
intro, all 9 minutes of the music is breathtaking.

Caffeine count - 2 tulsi masala chais, 1 filter coffee, 1 cold coffee, 1 black tea

## 2017 12 05, Tuesday

First day of the internship! Had a chat today with Julia (my mentor). We came
up with a list of 4 tasks for this week and then we meet again on Friday:

1. During the application period, I wrote a script to find all pairs of type (ATTRIBUTE\_DECLARING\_MACRO, ATTRIBUTE\_POSITION). There were 217 such pairs. Then, using these I went in the other direction and uncovered some 3500 undocumented sysfs attributes. Because my script did not account for regex, there might be some false positives. So, I'll spend a couple of days to refine the script.
2. At some places, the \_\_ATTR(...) macro is being used directly for attribute declaration. I should find out all usages and replace them with the more conventional DEVICE\_ATTR\_RO/RW(...) macros.
3. Send a Documentation/ABI patch to move one undocumented attribute to its right place and see how that goes.
4. Write a blog post on my Outreachy project, the motivations etc.

As I understand the documentation is not all for me to do. I am not equipped
with enough knowledge to fill in the documentation for all devices. The purpose
is to help others to find undocumented places and fill these gaps easily.

This should be helpful for people trying to set-up a device. They shouldn't
have to look-up the codebase to understand how to use it.

Lots to do this week.

Caffeine count: 2 tulsi masala chais, 1 black tea

## 2017 12 07, Thursday

Ported all of my scripts from python2 to python3 and uploaded them on Github:
https://github.com/aishpant/attribute-documentation

There are 2 main cocci scripts here:
1. Given a list of attributes documented in Documentation/ABI, it looks for all the declaring macros for them
2. Then using those declaring macros and the attribute position in the macros, we try to find all undocumented ones.

The first takes a lot of time to run. On driver code alone, it would take upto
16 hours to run on a VM with a single core. But I was happy to find that it
takes just 2 hrs 30 minutes now on a 4 core machine (using the -j numOfCores
flag on spatch). Furthur, using
[idutils](https://www.gnu.org/software/idutils/) gets the time down by 15-20
minutes.

Yesterday, I wrote another script that takes all the undocumented attributes
and greps for their usage in Documentation/ABI, If none is found, then
definitely these need to be ported. It's a list of about 900. I know that doing
this is not my work and is little help to what I want to do but it can help me
find some patterns. Kinda frustrating that I keep getting stuck here. But I can
use this data to send a patch for undocumented attributes (that I mention in my
weekly task).

I am now working on a script to convert raw \_\_ATTR calls to their DEVICE\_ATTR
counterparts. This is useful because it helps in readability of the code.
Should be done quickly.

Arch Linux is growing on me. The package managment system is very simple to
understand and works predictably.

[AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository)
[Pacman](https://wiki.archlinux.org/index.php/pacman)

Read 40 more pages of [From Heaven Lake by Vikram Seth](https://www.goodreads.com/book/show/50367.From_Heaven_Lake). I like how reading is progressing these days.

Caffeine count - 2 tulsi masala chais, 1 black tea

## 2017 12 08, Friday

spatch errors that I see frequently:

```
spatch -sp-file convert\_attr.cocci --dir ~/projects/linux/drivers/staging/ --use-idutils --debug
```
1.

```
@@
identifier foo, bar;
@@

- foo
+ bar
(...)

disjunction parenthesis in line 6 column 0 matched to normal parenthesis on line 7
```

Coccinelle treats column 0 of any line in a special way. So we should only put
characters on column 0 that we want to be treated specially like +, - , or
parentheses which are part of a disjunction (|). Error of this type can be
fixed by preceding the line with spaces.

2.

```
@@
identifier T, baz, foo, bar;
@@

struct T baz = {
 ...,
- foo
+ bar
 }

minus: parse error:
  File "convert\_attr.cocci", line 10, column 0, charpos = 78
  around = '',
  whole content =
```

The error thrown over here is not very helpful. It actually means that
coccinelle expects here a valid C statement. A statement like struct device dev = {..}
does not exist but struct dev = {...}; (followed by semi-colon) does.

Wrote a coccinelle script to convert \_\_ATTR macros to DEVICE\_ATTR in drivers.
Need to write another to convert DEVICE\_ATTR to DEVICE\_ATTR\_{RO/RW/WO} (these
are subcases).

Had another meeting with Julia. She was concerned about the number of falsely
positive macros. Suggested a technique to reward/penalise macros basis the
presence of the declared attributes in Documentation/ABI. Since I found some
220 macros and it will be cumbersome to look through all to rule out the bad
ones, this should decrease the size of the set.

## 2017 12 11, Monday

End of a long and tiring weekend.

Created a git repo for all cocci scripts:
https://github.com/aishpant/cocci-scripts

Sent a patch to replace \_\_ATTR in fbtft staging driver. Wrote a script to
convert DEVICE\_ATTR to file permission specific variants (uploaded to
cocci-scripts) and sent 2 patches using the same.

Finished the Vikram Seth novel.
