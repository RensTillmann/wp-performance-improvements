# Optimize wp_options table

**Query to see what the distribution looks like:**

  SELECT COUNT(*), autoload FROM wp_options GROUP BY autoload;


**If a large majority of them are set to 'no', we can solve the problem for now by adding an index on autoload:**

  ALTER TABLE wp_options ADD INDEX (`autoload`);


**Remove all _transient_ entries from wp_options table (It is 100% safe to optimize your table by removing all _transient_ entries. WordPress will generate new entries if requires in the future. Just use below query to optimize your wp_options table.
:**

	DELETE FROM `wp_options` WHERE `option_name` LIKE '_transient_%'
