# Members photos

My first cracking at querying RDF using SPARQL. I queried the Parliament beta website for all current Members' names and links to their new photos. 

code I used:


import rdflib

graph = rdflib.Graph()
graph.parse("https://api20170418155059.azure-api.net/fixedquery/house_current_members?house_id=KL2k1BGP")


#query the RDF using SPARQL, looking for all Members' full names and images
query = """
    SELECT ?o ?obj WHERE {
         ?s <http://example.com/A5EE13ABE03C4D3A8F1A274F57097B6C> ?o .
         ?s <http://id.ukpds.org/schema/memberHasMemberImage> ?obj
    }
    """
#print out the names and links to images. Had to replace URL of the image object in the RDF with the text of the publicly
#accessible API. Not sure if there is an easier way of getting at this link. Tacked .jpeg on the end of the link too.
for row in graph.query(query):
    initial = ("%s: %s" %(row[0],row[1]))
    print (initial.replace("http://id.ukpds.org/", "https://api20170418155059.azure-api.net/photo/")+".jpeg")

Take a look at the Ipython notebook for more information and the output from that code. You'll have to scroll past the first lot of RDF to get to the query that returns links to Members'photos.
