.. include:: ../Includes.txt

.. _best-practices-review:

=================================
Tips for contributors & reviewers
=================================

This page contains some general tips beyond the description of the workflow.

* :ref:`For new contributors <new-contributors-tips>`
* :ref:`For active contributors <tips-for-reviewers-and-active-contributors>`
  (related to reviewing patches)

.. index::
   single: Gerrit
   single: NewContributors

.. _new-contributors-tips:

Tips for new contributors
=========================

You are a new contributor. You found an issue in the core you wanted to
see fixed, you found a solution, you are satisfied with it, you
:ref:`setup your environment <setup>`, you figured out how to
:ref:`create a patch and push to Gerrit <Fixing-a-bug-A-Z>`,
you managed to :ref:`create a forge issue <bugreporting-index>` and you finally
pushed your patch.

Congratulations! That is great!

Now your patch is hanging around in the review queue on
`Gerrit <https://review.typo3.org/>`__ and either nothing
happens, it is voted down, people tell you your patch is not good enough
or suggestions are made to improve it and you don't know how.

Don't despair young padawan! The community around TYPO3 tries to act friendly
and helpful, we're not hurting anyone on purpose. We're open to anyone and
especially like to see new contributors and try to help getting them onboarded
and up to speed. Please consider the following things before becoming
frustrated or giving up:

* Most of the time spent on TYPO3 CMS core development is done for free.
  This gives contributors and reviewers freedom on what they work on.
  Unfortunately, this also means that sometimes a patch is not given the
  dedication it should receive.

* The review queue is often longer than the review power available.
  (See the dashboard on `Forger <https://forger.typo3.com/>` for the
  number of open reviews.) Sometimes patches are overlooked
  just because there is other hot stuff being worked on.

* Parts of the team usually work on something bigger. It may happen that some
  patches in the hot areas are merged very quickly while others do not get
  any attention. This is somehow natural and cannot be avoided since at any
  given time some reviewers usually focus on certain areas to get them right.

* Sometimes the whole team focuses on different stuff. For example, usually
  around "big" releases, the team focuses on bug fixing, so feature patches
  may get stuck for some time.

* Sometimes large parts of the active contributors are inactive at the same
  time. There are for example main holiday sessions with low overall activity.

* Sometimes getting little or no feedback on patches also has other reasons.
  Maybe the issue description is insufficient or not understood, maybe there is
  no documented way on how to reproduce a certain issue, or the bug or feature
  is bogus, or the issue is so complex and hard to solve that no one really
  wants to get their hands dirty on it.

What you can do to get feedback
-------------------------------

Here are some things you can do to raise awareness and get more feedback on
your patch and to help getting it reviewed (and eventually merged):

* Raise awareness: You are allowed to "ping" a patch once in a while. For
  example, you could :ref:`add a comment <Gerrit-Commenting-files>`
  "Hey, what is the status here, how to
  proceed with this patch?". This will raise the issue to the top in the
  queue and increases your chance of feedback. In general: Ask what is
  wrong, raise awareness, ask what is missing.

* Ask for help: Sometimes, issues can be solved in a better way if they are
  coordinated in direct chat. The TYPO3 CMS team uses Slack as
  instant communication platform. You are always welcome to join the
  #typo3-cms-coredev channel and ask for help on your pending patches.
  Please see :ref:`slack` for more information on how to join slack.
  Joining the #typo3-cms-coredev Slack channel usually helps sorting out
  things and gives a much better feeling on how the team works
  and what is going on.

How to improve your patch
-------------------------

It happens quite often that the first version of a patch
is not merged directly and needs a couple of patch sets before it is
finalized. In fact, merging "Patch Set 1" is the exception, and having
something merged in less than an hour is rather seldom. We're trying to
do things right, sometimes patches go through a whole lot of patch sets
and evolve in Gerrit until everyone is satisfied. This can take some time.

This is what you can do:

* Familiarized yourself with :ref:`Gerrit <Working-with-Gerrit>`.

* If reviewers make specific suggestions to improve your patch follow these
  suggestions and :ref:`upload another patchset <lifeOfAPatch-improve-patch>`.

* If you do not know what the suggestions mean or are unsure what to do, ask
  for help on :ref:`Slack <slack>` in the #typo3-cms-coredev channel.

* Act helpful and friendly: Chances are higher that your patch will be merged
  if the way you are communicating is fair. This is even more important for
  reviewers and active contributors, we do not allow ranters and haters in our
  team  and we try to stick to our
  `Code of conduct <https://typo3.org/community/code-of-conduct/>`__
  Please keep that in mind when working with us. You will be rewarded with
  the pleasure of working with a group of pretty smart people if you act
  accordingly.

* Don't get frustrated by -1 votes: Voting a patch down is a natural process
  in the review system and is not a sign that we hate you, your patch or your
  kitten. Our goal is to only merge things that are verified to be ready to
  go. A -1 basically blocks a patch from merging for a reason, and reviewers
  always add information on what is wrong or missing. Everyone wants to
  improve the system, so a -1 is just one method to achieve this.

.. _tips-for-reviewers-and-active-contributors:

Tips for reviewers and active contributors
==========================================

First, everyone is allowed to vote positive and negative on pending patches in
the Gerrit review queue for the TYPO3 CMS core product. We appreciate good
reviews on both code review and testing and this entry point was used by
quite some people already who were later nominated to be component or
framework mergers.

Frequently giving good reviews and improving patches is noticed and rewarded
and the team recognizes new helping hands. Another good entry point is joining
code sprints, look out for some if you have ambitions to be involved in core
development.

Acting as a reviewer and especially as an active contributor gives some
additional responsibility in dealing with the project and working with
other people in the review system. While technical discussions are
sometimes mastered with different opinions clashing each other, it is always
important to be respectful and fair to each other. There is no reason to act
rude just because some other reviewer has a different view to a specific point.

That being said, now some common guidelines and practical hints on reviewing habits.

Be helpful
----------

**Act especially helpful to newcomers!**

TYPO3 CMS is a living product and people join and leave the project. It is
important to welcome fresh blood and help them to get up to speed. Not every
effort in this area will be successful, but we must not scare away people
just because someone did something wrong with their first patches. Help
them to improve their patches: Fix commit messages, push new patch sets, add
forge tickets and give friendly hints of advice about problems with the
current state of patches and how to solve these problems.


Be honest
---------

Do not +1 a patch for review unless you have reviewed it or a +1 for tests
unless you have tested and verified that it resolves the issue.

See also the :ref:`policies on voting <gerrit-voting>`.

Do not merge hastily
--------------------

**Do not merge hastily after pushing a new version!**

Reviews of the final merged patch version are mentioned in the Git commit
message, reviewers of patches get karma by having their name in the core
commit log. This can be a nice motivator, so it is good habit to wait for
re-vote or to hint to people that they might like to re-vote if a last
version of a patch was pushed and the patch is close to being merged. Some
pages count successful votes on patches and have metrics for persons being
active in the project based on final reviews mentioned in the git log. Give
them a chance to get their review points, it is great to see those numbers.

Push new patchsets
------------------

**Don't be scared of pushing new patch sets!**

There are two different information on a merged patch set: The author of a
patch and the committer. Usually, the author of a patch is the person who
pushed the first patch set to gerrit, while the committer is the person
who finally pressed the merge button. When
:ref:`pushing new patch sets <lifeOfAPatch-improve-patch>`, the
author information is usually not overwritten, so you do not "steal"
the authors name by pushing new patch sets. However it *is* possible to
explicitly overwrite the author name with another name, but this is used
rarely and only if a patch changed so heavily that the person who pushes a
new patch set says "This is now my patch since it has nothing to do with
the initial version anymore". Usually, it is a good idea to keep the original
author name when updating a patch. This will happen correctly automatically if
a pending patch set from gerrit is :ref:`cherry-picked <cherry-pick-a-patch>`,
:ref:`amended and pushed <lifeOfAPatch-improve-patch>` in to
keep the original author information.

Decide about general issues before fixing nitpicks
--------------------------------------------------

**First, think about the solution itself and if that is ok, fix nitpicks!**

Core patches must follow our general :ref:`t3coreapi:cgl` to get maintainable,
readable and quickly understandable source code. In general, patches are not merged
before the CGL are followed.

However, if looking at patches, it is important to first answer these
questions:

* Is the issue itself relevant?
* Does the solution embed well in current development strategies?
* Is the architectural solution ok or is the patch just fixing some symptom
  instead of a different, maybe bigger problem?
* Does the solution contradict other patches we have in the same area?

So, first it should be decided if the architectural solution is fine. If that
is the case, the patch can then be optimized towards CGL needs. It happened
sometimes that a first patch was pushed, and some reviewers immediately started
doing nitpicks on CGL stuff, leading to tons of new patch sets until the patch
itself was codewise clean. After that, someone else showed up, looked at the
real issue and came to the statement that the solution itself is bogus. Such
things can easily kill motivation: Having a patch in the review queue, updating
it because of CGL stuff and later being voted down because of systematic concerns
about the solution after lots of energy was already put into the patch. It should
be the other way round: First align if a solution itself is accepted, and if that
is clear, do details like coding guidelines and minor improvements.

Fix CGL issues
--------------

**Fix CGL issues yourself instead of voting -1 for CGL issues!**

As said, we only want code merged that follows CGL. However, voting -1 because of
simple CGL violations can easily scare away people and kill motivation. Therefore
it is a very appreciated habit to not vote -1 because of CGL issues, but to
cherry-pick those patches, fix those issues and to push again, instead.

This has several positive side effects: A trained reviewer is used to quickly
cherry-pick, amend and push new patch sets anyway, so reading and fixing at the
same time usually takes less time than voting -1 and forcing someone else to
read through comments, apply and push again. And it will kill less motivation
for the patch committer who will not be forced to push again, wait for reviews,
push again, and so on, "just" because of CGL issues.

A friendly reviewer just fixes those issues on its own an pushes a new set, then
does the real review: "Hey, nice patch set. I like it and it works. Just pushed
a new version fixing minor CGL stuff. Would be cool if you read through my
changes compared to your version and if you try to follow those in the first
place next time. But your fix itself is great, I verified it and it works.
+1 for that, thank you!". Gives better karma, right?

As usual there are exceptions to those rules. Sometimes a reviewer has no time
to do those CGL fixes and decides to vote -1 instead, or maybe a patch is
codewise so ugly that is does not make much sense to put energy into that.
This is ok, just keep in mind that in general we appreciate minor issues to
be fixed by the reviewer directly.

Voting
------

Consider the :ref:`policies and tips for voting patches <gerrit-voting>`.


