# SQLContainer 概述

Web 應用一個重要的組成部分為訪問資料庫，Vaadin 提供的 SQLContainer 實現了 Container 介面用來連接各種資料庫。
SQLContainer 支持兩種類型的資料庫訪問，通過 TableQuery,使用這一預設的查詢生成器可以通過Container 介面直接讀取，更新，插入資料庫表格中。而使用 FreeformQuery 允許程序員使用自定義的查詢語句來讀取數據，並可以選擇實現如何寫入資料庫，過濾或者排序。
SQLContainer 支持使用 JDBC 連接或是 Java EE 連接池來連接資料庫。
SQLContainer 為 Vaadin Container 介面的一個實現，其中介面 Property 和 Item 的實現類為ColumnProperty 和 RowItem。 Item ID 則對應到 RowId 或是 TemporaryRowId 類。 RowId 的實現則基於資料庫的主鍵。

JDBCConnectionPool 定義 JDBC 連接池介面，Vaadin 內置兩個實現，一為SimpleJDBCConnectionPool 用於 JDBC 資料庫連接，而 J2EEConnectionPool 則用來連接 Java EE 數據源。

query 包定義了 QueryDelegate 介面， 定義了 SQLContainer 所需的 API 以支持資料庫的讀寫操作。 前面說過這個介面有兩個實現：一是 TableQuery ，另外一個是 FreeformQuery 。
query 包還定義了 Filter 和 OrderBy 類，可以支持 Container 的過濾和排序。
最後 generator 包定義了 SQLGenerator 介面，定義了類 TableQuery 所需要的一些查詢。 Vaadin 提供的支持包括 HSQLDB，MySQL, PostgreSQL (DefaultSQLGenerator), Oracle (OracleGenerator) 和 Microsoft SQL Server (MSSQLGenerator).
詳細的 API 定義可以參見 SQLContainer 文檔。

Tags: [Java EE](http://www.imobilebbs.com/wordpress/archives/tag/java-ee), [Vaadin](http://www.imobilebbs.com/wordpress/archives/tag/vaadin), [Web](http://www.imobilebbs.com/wordpress/archives/tag/web)