# Linkflows Model for fine-grained reviewing

An ontology for granular and semantic reviewing. 

Graphical representation with the online [WebVOWL](http://vowl.visualdataweb.org/webvowl.html) tool:
[Linkflows visualization](http://www.visualdataweb.de/webvowl/#iri=https://raw.githubusercontent.com/LaraHack/linkflows_model/master/Linkflows.ttl)

## Model description

The main class of the ontology is the *Comment* class, which includes review comments (subclass *ReviewComment*), on which we focus here, but the class also includes general text annotations or any kind of comment about a text snippet that comes with a dereferenceable URI.

The general properties of the model are *refersTo*, which connects a comment to the entity the comment is about, *isResponseTo*, which declares that a comment is a response to another comment, *isUpdateOf*, which connects an entity such as a comment to its previous version, *hasCommentText*, which links to the text content of a comment, and *hasCommentAuthor*, which declares the person who wrote a comment.

Our model defines three dimensions for review comments with different categories, each defined as subclasses of the class *ReviewComment*, which form the core of our semantic representation of reviews. 

The first dimension is about whether the point raised in the review comment is about individual spelling or grammar issues *SyntaxComment*), the general style of the text including text structure, text flow, text ordering, and consistent wording *StyleComment*), or the content of the text, e.g. about missing literature, the presented arguments, or the validity of the findings (*ContentComment*). 

The second dimension is the positivity/negativity of the review comment: *PositiveComment* for review comments that mainly raise positive points, *NeutralComment* for neutral or balanced points raised, and *NegativeComment* for the cases with mainly negative points. 

The third dimension captures whether an action is needed in response to the review comment (according to the reviewer): *ActionNeededComment* means that the reviewer thinks his or her comment necessarily needs to be addressed by the author; *SuggestionComment* stands for comments that may or may not be addressed; and *NoActionNeededComment* represents the comments that do not need to be addressed, such as plain observations. On top of that, we define a datatype property *hasImpact* that takes an integer from 1 to 5 to represent the extent of the impact of the point raised in the review comment on the overall quality of the article according to the reviewer. For negative comments this score indicates what would be the positive impact if the point is fully addressed, while for positive points it indicates what would be the negative impact if this point were not true.

To further clarify these dimensions and how they could be implemented in an actual reviewing system, we show a mockup of such an interface in ![Mock interface implementing the Linkflows model for reviewing](/images/logo.png). The entries reported in the interface correspond to the review dimensions identified in the model.

For representing the interaction between reviewers and authors and follow-up actions that are necessary or requested by the reviewer, the *ResponseComment* and *ActionCheckComment* were created as subclasses of *Comment*.
The author of the text snippet that was commented upon can agree, disagree, or partially agree with the review comment of the reviewer and they can indicate this classifying their response comment accordingly as *AgreementComment*, *PartialAgreementComment*, or *DisagreementComment*.

Finally, reviewers or editors can indicate in another follow-up comment whether they think that the author indeed addressed the point raised by the reviewer (to which they might have agreed, disagreed, or partially agreed). This can be expressed by the subclasses *PointAddressedComment*, *PointPartiallyAddressedComment*, and *PointNotAddressedComment*.
