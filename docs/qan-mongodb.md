# MongoDB specific

## Query Analytics for MongoDB

{{ mongodb }} is conceptually different from relational database management systems,
such as {{ mysql }} or {{ mariadb }}. Relational database management systems store data
in tables that represent single entities. In order to represent complex objects
you may need to link records from multiple tables. {{ mongodb }}, on the other hand,
uses the concept of a document where all essential information pertaining to a
complex object is stored together.

{{ qan }} supports monitoring {{ mongodb }} queries. Although {{ mongodb }} is not a relational
database management system, you analyze its databases and collections in the
same interface using the same tools. By using the familiar and intuitive
interface of QAN you can analyze the efficiency of your application
reading and writing data in the collections of your {{ mongodb }} databases.
