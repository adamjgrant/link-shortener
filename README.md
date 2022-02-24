# link-shortener

Using the free plans across Airtable, Cloudflare, and Github, you can make your own link shortener using a paid domain name.

## Instructions

### Airtable
1. Create an instance of the [Airtable base](https://www.airtable.com/universe/expzqYuzPyUwxLmTk/link-shortener)
2. Under the "Short URL" column, customize the formula so it uses your domain name.
3. If it wasn't created for you already, make an automation as follows:
   * Triggered on record create
   * Script step: Runs [this script](https://gist.github.com/adamjgrant/1d2dd774d257b8fa1ec8b57b4272224a). Make sure you set an input config variable called "id" to the "ID" field value from the previous step.
   * Update record step: Table: Links, Record ID: ID from first step, Fields: Code: Get code from previous step. You'll need to test the previous steps first.
   * Test this automation, then turn it on. If it works, you'll get the code field populated on each new row created.
4. Follow [the steps to make a read-only API key](https://support.airtable.com/hc/en-us/articles/360056249614-Creating-a-read-only-API-key).

### GitHub
1. Fork this repo.
2. In settings, activate pages using the main branch
3. Use [these instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) to set up your pages site for proper connection to the domain.

### Cloudflare
1. Create a new site pointed at your github pages repo (the one from the fork of this one). Use [these instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) if you need help connecting Cloudflare to the github repo.
2. In Rules, create a URL rewrite transform rule that matches the hostname (your domain), then rewrites the path to just "/" (leave the field blank). That's it. We're just making everything go to root so it hits the index.html in your fork.

If at first you don't succeed, give it about 20m, you may be waiting on Cloudflare/Nameserver updates to propagate.

Issues? File an one in this repo and I'll take a look.
