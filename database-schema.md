
## Database Schema Standards

* By default all tables should use InnoDB with a default character set of utf8.
* Table names must be in UpperCamelCase.
* Column names must be in lowerCamelCase.
* Table and Column names must be in singular form.
* Tables must have an auto-increment primary key named which is named after the table name ending in 'Id'.
 * Example: tableNameId, userId
* Tables must have a column indicating dateCreated and/or dateModified, as appropriate.
 * Both should be automatically handled by the database but if the version only supports one automatic then it should be the dateModified column.
* Column names must indicate content and/or usage.
 * Boolean fields must begin with preferably 'is' or alternatively 'has'.
  * Example: isEnabled, isDeleted, isStickied
 * Fields which reference primary keys in other tables must contain the full column name and can be optionally appended with a descriptive name to clarify content or disambiguate multiple usages.
  * Example: configId, userIdCreated, userIdModified
 * Fields which reference values in other tables should use FOREIGN KEYs. The index name in the declaration should be set to the name of the local field and should not use the value generated automatically.
 * Fields containing dates and/or times should be prefixed with date or time.
  * Example: dateCreated, dateModified, dateDeleted
 * Fields containing references to external data that may contain the word 'Id' in the column name must include the word 'External' to indicate as such.

