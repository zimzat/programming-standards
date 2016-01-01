
## Database Schema Standards

* By default all tables should use InnoDB with a default character set of utf8.
* Table names must be in UpperCamelCase.
* Column names must be in lowerCamelCase.
* Table and Column names must be in singular form.
* Tables must have an unsigned auto-increment primary key named which is named after the table name ending in 'Id'.
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

```sql
CREATE TABLE `User` (
	userId INTEGER UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
	dateCreated TIMESTAMP NOT NULL DEFAULT 0,
	dateUpdated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
	email VARCHAR(64) NOT NULL,
	role ENUM('guest') NOT NULL DEFAULT 'guest',
	isEnabled BOOLEAN NOT NULL DEFAULT TRUE,
	isDeleted BOOLEAN NOT NULL DEFAULT FALSE,
	UNIQUE INDEX email (email)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `UserAuthLogin` (
	userAuthLoginId INTEGER UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
	dateCreated TIMESTAMP NOT NULL DEFAULT 0,
	dateUpdated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
	userId INTEGER UNSIGNED NOT NULL,
	username VARCHAR(64) NOT NULL,
	password VARCHAR(255) NOT NULL,
	UNIQUE INDEX userId (userId),
	UNIQUE INDEX username (username),
	FOREIGN KEY userId (userId)
		REFERENCES User (userId)
		ON UPDATE CASCADE
		ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

