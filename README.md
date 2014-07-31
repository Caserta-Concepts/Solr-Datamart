#Solr Datamart

**Companion materials for our [BDW Meetup](http://www.meetup.com/Big-Data-Warehousing/events/194134322/) on this topic.**
###Overview:
Although Solr was primarily architected as a search engine, there is no reason you can’t use it as a database.  In fact it makes an excellent analytic database, providing excellent performance and rich/flexibile query syntax.  

This repo is setup to help anyone interested in learning more about Solr get started quickly with some sample Yelp data.


###Setup
1. Install Solr - `brew install solr`
2. Rename existing schema.xml under the following path and replace with the one provided in this repo `/usr/local/cellar/solr/4.8.1/libexec/example/solr/collection1/conf`
3. Change Directories: `cd /usr/local/cellar/solr/4.8.1/libexec/example`  and Start Solr: `java -jar start.jar`, leave this window open.
4. Open another terminal and change directories: `cd /usr/local/cellar/solr/4.8.1/libexec/example/exampledocs`
5. Unzip and post sample data: `java -Durl=http://localhost:8983/solr/collection1/update -Dtype=text/csv -jar post.jar /Users/elliottcordo/Downloads/yelp_solr.csv000`
  
**Note windows or linux users will need to install using OS specific instructions, see Apache site for details.**

If you want to install Banana visit the LucidWorks repo [here](https://github.com/LucidWorks/banana). Follow build and setup instructions. 


###You should be up and running?!?  
* Browse to the admin:
`http://http://localhost:8983/solr/admin/`
* Try a simple query: `http://localhost:8983/solr/collection1/select?q=city:Yuma&wt=json&indent=true`  
* A simple "group by": `http://localhost:8983/solr/collection1/select?q=state:AZ&wt=json&indent=true&facet=true&facet.field=city&rows=0&facet.mincount=1&facet.limit=-1`
* Facet Stats: `http://localhost:8983/solr/collection1/select?q=state:AZ+review_date:%5B2012-03-01T23:59:59.999Z%20TO%202012-03-06T00:00:00Z%5D&wt=json&indent=true&facet=true&rows=0&facet.mincount=1&facet.limit=-1&stats=true&stats.field=stars&stats.facet=city`

###Other helpful stuff:
* If you change your schema you must restart solr and reload your data
* Collection/Core = Database
* Facet is a "Cube/Olap" type structure used for navigation...  
* Learn U some Solr query syntax [here](https://wiki.apache.org/solr/SolrQuerySyntax)
* how to delete all data from your index, note dummied the core name to prevent you accidentally clearing!:
  
`http://localhost:8983/solr/YOUR CORE HERE/update?stream.body=<delete><query>*:*</query></delete>`

`http://localhost:8983/solr/YOUR CORE HERE/update?stream.body=<commit/>`

