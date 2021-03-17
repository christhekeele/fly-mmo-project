Fly Developer Content Guidelines
================================

The Fly Voice
-------------

TBD

Brand Presentation
------------------

### The Platform

When referring to the platform in any context, use "Fly", rather than:

- "fly"
- "fly.io"
- "the platform"

### The Tooling

When referring to the CLI in any context, use `flyctl`, rather than:

- "flyctl"
- `FlyCtl`
- "the CLI"

Content Presentation
--------------------

### Content Types

The concept of individuals having preferred "learning styles" (ie the VARK model: Visual, Auditory, Reading, Kinetic) is not well-supported by science. However, it is well established that having *multiple avenues* to learn the same concept improves understanding. "Learning styles" are a still a ***useful*** model for thinking about different ways to present the same concept: people learn better when there are several modes with which they can interface with concepts.

Most developer content we want to produce can be showcased in more than one way, loosely matching these learning styles:

- Reading: Written Content
  
  This is our main mode of interaction, spanning technical docs, narrative articles, and support forums.

- Visual: Reference Code

  In the context of programming, reference code is our "visual" content, from code snippets to example repositories.

- Kinetic: Deployable Demos

  Fly is an application platform, so we should find ways for most content to lead to deployable projects.

- Auditory: 

  This mostly fits meetup/podcast/conference talk content, which we don't have a strategy for — yet.
  

#### Written Content

These are the articles we publish. There are three flavors: reference material, narrative material, and community material.

##### General Tips

We should ***never*** make assumptions about the reader's comfort level with just about anything beyond the immediate context. This includes:

- Assuming in the Fly overview docs they know about `flyctl`
- Assuming in the `flyctl deploy` docs they know about `flyctl scale`
- Suggesting they should be as fluent as the author in performing any action with "confidence adjectives". These are easy to accidentally include, but we should AVOID phrases like:
  - "...***simply*** run `brew install flyctl`..."
    - prefer: "...run `brew install flyctl`..."
  - "...***just*** update the dependencies..."
    - prefer: "...update the dependencies via `npm update`..."
    - prefer: "...update the dependencies [link to documentation]..."

##### Reference Material

Reference material concerns things like technical documentation found in our [product docs](https://fly.io/docs), or the help text from `flyctl`.

It should favor the imperative without a subject (ex "**Deploy** to Fly") when we are instructing developers, and fall back to using the second-person singular voice when needed as if we are talking directly to them (ex "...if **you** run into issues...").

This sort of content should be dry: we do not affect the Fly "voice" here, as people may be reading it in anger and it is not the time to try to be engaging.

##### Narrative Material

This is generally any content we author meant to engage developers within the confines of our publishing platform, including blog posts and guides (as opposed to reference material).

It should favor the second-person plural voice (ex "...next, **we** provision a volume...") as if we are accomplishing the feats of the article together.

This ***is*** our opportunity to demonstrate the Fly "voice" and draw people into the product and our ecosystem.

This sort of content should be laser-focused on **telling a single story** (though you may not yet know that story when you begin writing!) Ideally all such articles include a (private, unpublished) *précis* that describes this story: the journey the reader will follow when reading it, and how they will have been changed by it when they arrive at its destination.

##### Community Material

Written material that forms a dialog with other developers can be thought of as community material. This includes communications on our own support channels, as well as any discussion on other platforms.

Here we should favor the first-person singular (ex "...when **I** last had that problem...") as we are peers in a discussion, even if we may be implicitly representing the whole of Fly in certain contexts.

The voice used here should be your own, bearing in mind that you are acting as an ambassador of our company and interacting directly with our customers! Find opportunities to:

- be understanding, rather than being judgemental
- admit uncertainty, rather than being defensive
- mirror excitement, rather than being dry

###### Support Communications

Any interaction with someone who needs help with using Fly should be treated as a support context, no matter the platform. In general apply these tips to any community interaction; but especially in support contexts, try to:

- acknowledge frustration, before moving on to trying to help solve problems
- speak about certainties, rather than responding with speculation
- reference helpful canonical content, rather than re-explaining everything on the fly

#### Reference Code

These are the repositories we share. 

Discuss code repo strategies here

