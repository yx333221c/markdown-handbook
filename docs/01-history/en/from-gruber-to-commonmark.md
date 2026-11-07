# From Gruber to CommonMark

> 中文: [zh/from-gruber-to-commonmark.md](../zh/from-gruber-to-commonmark.md)

Gruber's canonical syntax description tells you how to write Markdown. It doesn't settle the edge cases, and it was never an unambiguous spec. How many spaces indent a nested list? Do you need a blank line before a block quote? Which of two link definitions with the same name wins? Section 1.3 of the GFM spec later listed a whole run of questions it left open.

Early implementers had one place to look when they got stuck: the source of `Markdown.pl`, a Perl script with bugs of its own. Each author filled the gaps differently. Ten years produced dozens of implementations, and the same document could come out one way in a GitHub wiki and another when Pandoc turned it into docbook.

Markdown has no syntax errors. CommonMark puts it bluntly: any sequence of characters is a valid document. You write a list you're sure is fine, the renderer hands you HTML, and the only sign of trouble is that the paragraph nesting differs from someone else's. Nothing fails loudly. You notice when the document moves to another platform, or when a diff fills up with formatting changes. Babelmark lines up the output of more than 20 implementations so you can see the splits.

On 2012-10-25 Jeff Atwood published "The Future of Markdown". He asked the big sites to agree on a formal spec and a test suite, and mentioned an email from David Greenspan plus a working name, "Rockdown". In 2014 John MacFarlane, David Greenspan (Meteor), Vicent Marti (GitHub), Neil Williams (Reddit), Benjamin Dumke-von der Ehe (Stack Exchange) and Jeff Atwood (Discourse), among others, started the project that became CommonMark. The CommonMark site now lists John MacFarlane, Martin Woodward and Jeff Atwood as core members.

The spec carries version numbers, `0.29` and `0.30` (2021-06-19) among them. I won't call any of them current, since the number moves on and the page will likely have changed by the time you read this. The site lists Discourse, GitHub, GitLab, Reddit, Qt, Stack Overflow / Stack Exchange and Swift as adopters.

People argued about it. Some thought a spec hundreds of pages long was the wrong answer for a syntax sold on being readable, and the wording does clash with Gruber's page: CommonMark states plainly that any sequence of characters is a valid document. The concrete disagreement lives in the spec text and in the implementations. I have no record of what Gruber said about it, so I'm not putting words in his mouth.

For the spec itself, see [CommonMark](../../03-spec/en/commonmark.md); for GitHub's dialect, [GFM](../../03-spec/en/gfm.md).
