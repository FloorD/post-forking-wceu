#Working on post-forking for WordCamp Europe 2013

For [my WordCamp Europe 2013 talk](http://www.1stfloorgraphics.nl/2013/10/06/working-towards-great-version-control-for-content-creators-talk-excerpt-wceu-2013/) I looked into WordPress plugins handling version control. As [Post Forking](http://wordpress.org/plugins/post-forking/) extends WordPress's native Diff system to allow three-way merges (similar to Git) and generally comes close to what I'd want talking version control for content creators, I decided to work on Post Forking during the contributors day. 

WordPress Post Forking allows users to "fork" or create an alternate version of content to foster a more collaborative approach to WordPress content curation. This can be used, for example, to allow external users (such as visitors to your site) or internal users (such as other authors) with the ability to submit proposed revisions. It can even be used on smaller or single-author sites to enable post authors to edit published posts without their changes appearing immediately. 

Post Forking compares the original (pre-fork) post, the fork, and the current (live) version of the post to determine what, if anything has changed in the fork that is not reflected in the post, and merges the fork back back into the parent post. If the merge is clean, WordPress will merge the fork back into the post. If not, it will note the conflict and present it to the user for a decision. 

Conflicts are notated similar to git merge conflicts using ```>>>>>>```, ```======```, and ```<<<<<<``` markings within the body of the fork. The merger is then presented with the ability to resolve the conflict manually. As such the plugin borrows some concepts from decentralized version control systems like Git, but **the underlying technology is still just WordPress's normal revision system**. When a user without the ```edit_post``` capability attempts to edit a given post, WordPress will automatically create a "fork" or alternate version of the post which they can freely edit. The fork goes into the standard WordPress moderation queue (just like any time an author without the ```publish_post``` capability submits a post), where an editor can review, and potentially approve the changes for publishing. 

Only certain fields (e.g., ```post_content```, ```post_title```) are copied over to the new fork. 
The plugin also stores the revision ID for the revision prior to when the fork was created (```includes/revisions.php```). Publishing a fork (either by the fork author, if they have the capability, or my an editor) triggers the merge itself. The post content of the fork undergoes a three way merge with the base revision and current version of the parent post.
No user should have the ```edit_published_fork``` capability. Once published, the fork post_type simply exists to provide a record of the change and allow the author page, to theoretically list contributions by author. 

Allowing users without edit or publish post capabilities to edit and submit changes to content (similar to GitHub’s pull request system)
Collaborative editing (by resolving two users’ conflicted saves – Wired’s example)
Saving draft changes of already-published content
Scheduling pending changes to already-published content


**Post** - Any WordPress post that uses the ```post_content``` field, including posts, pages, and custom post types  
**Fork** - Clone of a post intended for editing without disturbing the parent post  
**Branch** - Parallel versions of the same parent post, owned by the post author  
**Merge** - To push a fork's changes back into its parent post  
**Conflict** - When a post is forked if a given line is changed on the fork, and that same line is subsequently edited on the parent post prior to the merge, the post cannot be automatically merged, and the conflict is presented to the merger to resolve  

##post-forking roadmap 

- Front end editing (just click edit, make your change, hit submit)  
- Ability to fork more than just the post_content (e.g., taxonomies, post meta)  
- [Appending parent revision history to fork](https://github.com/benbalter/post-forking/issues/15)  
- Spoofing post_type so metaboxes, etc. appear  
- [Author pages for fork contributors](https://github.com/benbalter/post-forking/issues/17)  
- [Open Enhancements](https://github.com/benbalter/post-forking/issues?labels=enhancement&page=1&state=open)  


##My wish list

**Showing updates and attribute them**  
This was actually a request from the WordCamp Europe audience, but I could not agree more. Providing an interface to show updates (with time stamps!) and attributing them to authors, to give more transparency in how the article is crafted.

Making sure that all the meta-data (revisions, authors, …) are fully searchable.

**commenting in post draft**  
Commenting on changes, both your own' and others, helps to get everyone in the project on the same page - quite literally. You might want to explain why you deleted a whole paragraph, or why you find that cat picture less fitting. Rather than  using email for such things, why not keep it in one place? Your plugin installation / WordPress dashboard.  

**Task lists (issues) with assigning possibilities**  
Task lists (issues) with assigning possibilities. Why use a bug trackers, a project management tool... and WordPress, right? Ok, for smaller blogs this might not even a pressing issue, but imagine if it would be possible!  

**issues / task list**  
Listing 'post requests', or 'update requests' and assigning them to team mates. 

**key words**  
Using key words in/as post requests, fully searchable (and visible in the excerpt view - editor) - although this might be feature freaking for this particular plugin.  
Other good stuff in that line of thinking: save and show alternative titles (previous titles greyed out/in a drop-down, and autocomplete). 

**Notifications?**  
I'd like to receive notifications when my blog mates sign of a change or respond to text that I've written or altered. Same goes for issues/tasks that get added and pull requests that get... pulled? But maybe I'm feature freaking here.   

Added to the issue list.  

##Log

I look at:  
```#97``` - [Manual merging page should include instructions](https://github.com/post-forking/post-forking/issues/97)   
```#38``` - [Labels confusing for non technical users](https://github.com/post-forking/post-forking/issues/38)  

**[editing any content or creating additional pages](https://github.com/benbalter/post-forking/wiki):**  
- [Features and Overview](https://github.com/benbalter/post-forking/wiki/Description)  
- [FAQ](https://github.com/post-forking/post-forking/wiki/Frequently-Asked-Questions)  

My post-forking mate [Christoph](http://twitter.com/ssstofff) works on nl/be [translations](http://translations.benbalter.com/) and Frank worked on [open issues](https://github.com/post-forking/post-forking/issues/). 
