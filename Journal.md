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

```c
spatch -sp-file convert_attr.cocci --dir ~/projects/linux/drivers/staging/ --use-idutils --debug
```
1.

```c
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

```c
@@
identifier T, baz, foo, bar;
@@

struct T baz = {
 ...,
- foo
+ bar
 }

minus: parse error:
  File "convert_attr.cocci", line 10, column 0, charpos = 78
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

## 2017 12 12, Tuesday & Wednesday

Last couple of days. Fail and try a few things.

I've got two variants of the scripts for converting DEVICE_ATTR to
file permission specific ones.

Here is one which converts declaration and renames show/store functions:

```c
@r@
identifier attr, show_fn;
declarer name DEVICE_ATTR;
@@

DEVICE_ATTR(attr, \(S_IRUGO\|0444\), show_fn, NULL);

@script: python p@
attr_show;
attr << r.attr;
show_fn << r.show_fn;
@@

// standardise the show fn name to {attr}_show
coccinelle.attr_show = attr + "_show"
print (show_fn)
@@
identifier r.attr, r.show_fn;
declarer name DEVICE_ATTR_RO;
@@

// change the attr declaration
- DEVICE_ATTR(attr, \(S_IRUGO\|0444\), show_fn, NULL);
+ DEVICE_ATTR_RO(attr);

@rr@
identifier r.show_fn, p.attr_show;
@@

// rename the show function
- show_fn
+ attr_show
        (...) {
        ...
  }

@depends on rr@
identifier r.show_fn, p.attr_show;
@@

// rename fn usages
- show_fun
+ attr_show
```
And then, there is type 2 which converts only when show/store function
names match the specification:

```c
@r@
identifier attr, show_fn;
declarer name DEVICE_ATTR;
@@

DEVICE_ATTR(attr, \(S_IRUGO\|0444\), show_fn, NULL);

@script: python p@
attr << r.attr;
show_fn << r.show_fn;
@@

if (attr + '_show' != show_fn):
        cocci.include_match(False)

@@
identifier r.attr, r.show_fn;
declarer name DEVICE_ATTR_RO;
@@

// change the attr declaration
- DEVICE_ATTR(attr, \(S_IRUGO\|0444\), show_fn, NULL);
+ DEVICE_ATTR_RO(attr);
```

This is safer to use as sometimes show/store functions are shared.

I only sent a patch for staging drivers where the safer script was
applicable. I'm not not sure if it would be welcome elsewhere as it's
just a cleanup.

I'm tracking cocci scripts in this repo :
[cocci-scripts](https://github.com/aishpant/cocci-scripts)

Julia suggested a method for reducing false postives where I mark
up/down macros if the corresponding attributes are found/not-found in
the documented sysfs attributes (since some attributes have very common
names- id, dev etc).

That did not work very well. So what I actually did was to look through
macro names which did not have the word 'attr' or 'attribute' in them
and manually ruled out the ones which were not attribute declarers (~20).

And then I found a bug. To find the list of undocumented attrs, I was
looking at the symmteric difference of found_attrs and documented_attrs.
This is incorrect. Changed it to a set difference between found_attrs
and documented_attrs. That brought down the number from ~2000 to ~900.
These are stored in [result/undocumented_attrs.txt](https://github.com/aishpant/attribute-documentation/blob/master/result/undocumented_attrs.txt)

## 2017 12 14, Thursday

Now, there is a massive problem with the script I have got. Finding
undocumented attributes is not really the point, I need to find the complete
sysfs path for a device/driver as the names themselves don't have to be unique.

For eg, an attribute like volume could be present for two different attributes
but documented for one and not the other.

I need to track down how I can get from the attribute declaration to the path
and update the searching process to take the path into account.

Exciting stuff!

This is really tricky now. There are numerous ways and preferred ways of adding
files and folders to the sysfs hierarchy.

```c
# add a folder to the path (non-dynamic)
# /sys/kernel/kobject_example
example_kobj = kobject_create_and_add("kobject_example", kernel_kobj)

# create the files associated with the object, the attrs in attr_group fall
# under /sys/kernel/kobject_example/{attr}
sysfs_create_group(example_kobj, &attr_group);
# add one attr file
sysfs_create_file(example_kobj, attr);
# add multiple attrs files
sysfs_create_files(example_kobj, &attr_group);

# expose binary attribute
int sysfs_create_bin_file(struct kobject *kobj, struct bin_attribute *attr);

# create symbolic links
int sysfs_create_link(struct kobject *kobj, struct kobject *target, char *name)

# bus, device, driver registration
BUS_ATTR(name, mode, show, store);
int bus_create_file(struct bus_type *bus, struct bus_attribute *attr);

# device registration
DEVICE_ATTR(name, mode, show, store);
int device_create_file(struct device *device,
                       struct device_attribute *entry);

```

Chapter-14 from Linux Device Drivers (The Linux Device Model) and the code in
scripts/kobject/kobject-example.c helped me understand the formation of the
hierarchy. I am going to look into The Linux Programming Interface as well.

I'm going to read up the chapter again and then write a kernel module to
document the various ways in which you can expose sysfs attrubutes.

Julia asked me create a spreadsheet of all non-documented attributes and along
with info about where and how they declared and whether they are documented but
outside of Documentation/ABI. It seems like we will be focusing on moving
documentation that is already there to the right place.

Trivia: the manpage for sysfs was created as recently as September 15, 2017 and
was part of the 4.13 release. (man 5 sysfs)

Caffeine count: 1 filter coffee, 2 tulsi malasa chais

## 2017 12 21, Thursday

A week in which not much happened. For the next 7 days, I will be in Pune.

Added a [table on undocumented
attributes](https://github.com/aishpant/attribute-documentation/blob/master/result/output.csv)
with some more info. There are 4 columns here - attribute name, macro, filename,
is somewhere in Documentation.

The last column for now has two values- either Maybe or No. Maybe means that a
simple grep for the attribute name in Documentation/\* produced a match and No is
the opposite.

The sysfs implementations of drivers is quite complex and varied. I started
writing the module and realised it is not a real representation. So I decided to
look at how class subsystem attributes are defined and then walk backwards from
it.

Julia and I had another meeting yesterday. The focus of this week is on
documenting hwmon in ABI.

For eg. all of hwmon driver attributes are documented quite nicely in
Documentation/hwmon/sysfs-interface and in the driver specific files.

```
Documentation/hwmon/sht3x:

sysfs-Interface
---------------

temp1_input:        temperature input
humidity1_input:    humidity input
temp1_max:          temperature max value
...
```
This is not in the ABI subdirectory and is not in the format used there.

Second focus is on writing a module to document class interface. It just so
happens that discovering devices through class interface is the easiest. And
most drivers including hwmon follow this standard. class interface allows you to
work with devices based on what they do, rather than how they are connected or
what they do. hwmon (hardware monitoring) is built into the kernel and you can
access it from /sys/class/hwmon/hwmon[0-\*].

If I had to discover all the hwmon devices from sysfs, this is how I would do
it:

```bash
find /sys/ -name '*hwmon*'

/sys/devices/platform/coretemp.0/hwmon
/sys/devices/platform/coretemp.0/hwmon/hwmon2
/sys/devices/virtual/hwmon
/sys/devices/virtual/hwmon/hwmon0
/sys/devices/virtual/hwmon/hwmon1
/sys/class/hwmon
/sys/class/hwmon/hwmon2
/sys/class/hwmon/hwmon0
/sys/class/hwmon/hwmon1
/sys/module/hwmon_vid

ls -al /sys/class/hwmon

total 0
drwxr-xr-x  2 root root 0 Dec 21 16:54 .
drwxr-xr-x 57 root root 0 Dec 21 16:54 ..
lrwxrwxrwx  1 root root 0 Dec 21 17:02 hwmon0 -> ../../devices/virtual/hwmon/hwmon0
lrwxrwxrwx  1 root root 0 Dec 21 17:02 hwmon1 -> ../../devices/virtual/hwmon/hwmon1
lrwxrwxrwx  1 root root 0 Dec 21 17:02 hwmon2 -> ../../devices/platform/coretemp.0/hwmon/hwmon2
```

Step-1 for writing classes : Create an instance of struct class. Name here is
'hwmon'.

```c
static struct class hwmon_class = {
	.name = "hwmon",
	.owner = THIS_MODULE,
	.dev_groups = hwmon_dev_attr_groups,
	.dev_release = hwmon_dev_release,
};

```

Managing classes:

```c
int class_register (struct class *cls);
void class_unregister (struct class *cls);
```

```c
static int __init hwmon_init(void)
{
	int err;

	hwmon_pci_quirks();

	err = class_register(&hwmon_class);
	if (err) {
		pr_err("couldn't register hwmon sysfs class\n");
		return err;
	}
	return 0;
}

static void __exit hwmon_exit(void)
{
	class_unregister(&hwmon_class);
}
```

Defining class attributes (not widely used):

```c
CLASS_ATTR(name, mode, show, store);
int class_create_file(struct class *cls, const struct class_attribute *attr);
```

There is a paper on sysfs from [2005](https://www.kernel.org/pub/linux/kernel/people/mochel/doc/papers/ols-2005/mochel.pdf). Very introductory optimistic paper.

What really is udev? And how does it use uevents?

[Kernel Recipes 2016 - The Linux Driver
Model](https://www.youtube.com/watch?v=AdPxeGHIZ74)

This talk by Greg is an update on the Ch-14 of Linux Driver Drivers.

Summary:

You never really need to work with or know internals of kobjects, or ksets or
kobj\_type. These are fundamental objects (like base classes of OOP) emebedded
in other high level objects.

Relevant for driver writers-
1. Use only attribute groups for exposing sysfs attributes.
2. Never use any of the sysfs\_\* functions or work with kobjects except for
   maybe the sysfs\_notify function
3. Never use platform\_device
4. Use a class or bus interface and not deal with raw kobjects to avoid
   boilerplate code. class\_create() and class\_destroy()

The userspace APIs are a huge mess. No one really knows how to use them well and
they keep evolving. I keep seeing a different implementation in every driver. This is
taking much much longer than expected.
Most every day I do these things:

1. Read a lot of code and understand a little
2. Run git grep on some API from LDD and find that it's deprecated
3. Run a lot of git grep. I checked my command line history and found out that I
   ran git grep 347 times in 3866 commands or ~9% of the time
4. Look for articles/discussions/conference talks on the device model and the
   kernel userspace API. LWN is the best resource but I would not recommend
   anyone to use their search API (P.S. it's the worst)
