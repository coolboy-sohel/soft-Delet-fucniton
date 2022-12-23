# Soft Delete Plugin for MongoDB

This plugin provides a way to "soft delete" documents in a MongoDB collection, rather than permanently deleting them. When a document is "soft deleted", it is not removed from the collection, but rather, a deletedAt field is added to the document with the current timestamp.

# Installation

To install the plugin, you will need to have MongoDB installed on your system. Then, follow these steps:

Download the latest release of the plugin from the releases page.
Extract the contents of the downloaded archive.
Navigate to the extracted directory in your terminal.
Run the following command to install the plugin:

mongod --install --dbpath <path/to/data/directory>

Replace <path/to/data/directory> with the path to your MongoDB data directory.

# Usage
To use the plugin, simply include the deletedAt field in your MongoDB documents and use the $set operator to update the field when you want to "soft delete" a document.

For example, the following code will "soft delete" a document with the _id of 123 in the users collection:

Copy code
db.users.update(
  { _id: 123 },
  { $set: { deletedAt: new Date() } }
)
To retrieve only non-deleted documents, you can use the following query:

Copy code
db.users.find({ deletedAt: { $exists: false } })
# Limitations
Please note that the deletedAt field is not indexed by default, so queries with a condition on the deletedAt field may not perform as well as queries without this condition. If you anticipate needing to perform frequent queries based on the deletedAt field, you may want to consider adding an index on this field.

# Contributions
We welcome contributions to the Soft Delete plugin. If you have an idea for a new feature or have found a bug, please open an issue on the GitHub repository. If you would like to submit a pull request with a fix or new feature, please follow these guidelines:

Fork the repository and create a new branch for your changes.
Make sure your code is properly formatted and passes the linter (run npm run lint to check).
Add tests for any new functionality.
Make sure all tests pass (run npm test to check).
Submit your pull request and include a description of your changes.
# License
The Soft Delete plugin is licensed under the MIT License. See LICENSE for more details.
