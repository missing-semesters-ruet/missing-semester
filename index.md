---
layout: page
title: "The Missing Semesters of Your CS: RUET"
nositetitle: true
---

<div class="note">
This document has been modified from the <a
href="https://missing.csail.mit.edu/"> original site</a> developed by MIT to be more relevant to RUET's Missing Semesters Community.  
<br />
The full history of our changes can be viewed <a href="https://github.com/missing-semesters-ruet/missing-semester">here</a>.
<br /><br />
<em>This</em> Missing Semester is brought to you by <a href="https://github.com/shafayetsadi">Shafayet Sadi</a> and <a href="https://github.com/md-tonmoy007">Tonmoy Jifat</a>.
<br />
Boxes like this will indicate notes added by us.
</div>

Classes teach you all about advanced topics within CS, from operating systems
to machine learning, but there’s one critical subject that’s rarely covered,
and is instead left to students to figure out on their own: proficiency with
their tools. We’ll teach you how to master the command-line, use a powerful
text editor, use fancy features of version control systems, and much more!

Students spend hundreds of hours using these tools over the course of their
education (and thousands over their career), so it makes sense to make the
experience as fluid and frictionless as possible. Mastering these tools not
only enables you to spend less time on figuring out how to bend your tools to
your will, but it also lets you solve problems that would previously seem
impossibly complex.

Read about the [motivation behind this class](/about/).

# Practicalities

**Please register and join the discord!**

-   **Registration**: [Registration form](https://forms.gle/tyXjuXrVpZfsBDRh8)
-   **Questions / Discussions**: Please join the [Missing Semesters-RUET Discord](https://discord.gg/)!
-   **Time/Location**:
    -   **Semester 1**: Thursdays 10:00-12:30 in Odd Semesters
    -   **Semester 2**: Thursdays 10:00-12:30 in Even Semesters
-   **Facilitators**: MS is run by Students of ECE and CSE, with support from Department of ECE.

# Schedule

<ul>
{% assign lectures = site['2025'] | sort: 'date' %}
{% for lecture in lectures %}
    {% if lecture.phony != true %}
        <li>
        <strong>{{ lecture.date | date: '%-m/%d/%y' }}</strong>:
        {% if lecture.ready %}
            <a href="{{ lecture.url }}">{{ lecture.title }}</a>
        {% else %}
            {{ lecture.title }} {% if lecture.noclass %}[no class]{% endif %}
        {% endif %}
        </li>
    {% endif %}
{% endfor %}
</ul>

# About the class

**Staff**: This course is co-taught by [Shafayet Sadi](https://www.github.com/shafayetsadi), [Tonmoy Jifat](https://github.com/md-tonmoy007), and students of ECE and CSE.<br>
**Questions**: Email us at [missingsemesters.ruet@gmail.com](missingsemesters.ruet@gmail.com).

# Related Resources

<div class="note">
Please note -- these links pertain only to the original MIT content which may have been altered.
</div>

Video recordings (of the original MIT lectures) are available [on YouTube](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J).

You can find posts and discssions on:

-   [Hacker News](https://news.ycombinator.com/item?id=22226380)
-   [Lobsters](https://lobste.rs/s/ti1k98/missing_semester_your_cs_education_mit)
-   [/r/learnprogramming](https://www.reddit.com/r/learnprogramming/comments/eyagda/the_missing_semester_of_your_cs_education_mit/)
-   [/r/programming](https://www.reddit.com/r/programming/comments/eyagcd/the_missing_semester_of_your_cs_education_mit/)
-   [Twitter](https://twitter.com/jonhoo/status/1224383452591509507)
-   [YouTube](https://www.youtube.com/playlist?list=PLyzOVJj3bHQuloKGG59rS43e29ro7I57J)

# Translations

-   [Bengali](https://missing-semester-bn.github.io/)

<div class="note">
Note: these are external links to community translations. We have not vetted
them.
</div>

Have you created a translation of the course notes from this class? Submit a
[pull request](https://github.com/missing-semester/missing-semester/pulls) so
we can add it to the list!

## MIT Acknowledgements

We thank Elaine Mello, Jim Cain, and [MIT Open
Learning](https://openlearning.mit.edu/) for making it possible for us to
record lecture videos; Anthony Zolnik and [MIT
AeroAstro](https://aeroastro.mit.edu/) for A/V equipment; and Brandi Adams and
[MIT EECS](https://www.eecs.mit.edu/) for supporting this class.

---

<div class="small center">
<p><a href="https://github.com/missing-semester/missing-semester">Source code</a>.</p>
<p>Licensed under CC BY-NC-SA.</p>
<p>See <a href="/license/">here</a> for contribution &amp; translation guidelines.</p>
</div>
