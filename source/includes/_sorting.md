# Sorting

Our APIs supports requests to sort resource collections according to one or more criteria usin a `sort` query parameter. The value for `sort` must represent the object attributes.

We support **multiple sort attributes** by using comma-separated "," attributes. Sort attributes are applied in the order specified.

The sort order for each sort attributes is **ascending by default** unless it is prefixed with a minus "-", in which case it is **descending**.
