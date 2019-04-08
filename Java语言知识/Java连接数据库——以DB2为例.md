# Java连接数据库——以DB2为例

```java
package db2.conn;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class simpleConnDB2 {

	public static void main(String[] args) throws ClassNotFoundException, SQLException {
		// 1.加载DB2驱动程序类
		Class.forName("com.ibm.db2.jcc.DB2Driver");
		// 2.获取数据库连接
		Connection conn = DriverManager.getConnection("jdbc:db2://localhost:50000/testdb", "db2admin", "123456");
		// 3.定义查询语句
		String sql = "select * from usertable";
		// 4.创建Statement对象
		Statement stmt = conn.createStatement();
		// 5.执行查询语句并获得查询结果集
		ResultSet rs = stmt.executeQuery(sql);
		// 6.遍历查询结果集
		while (rs.next()) {
			int id = rs.getInt(1);
			String user = rs.getString(2);
			String password = rs.getString("password");
			System.out.println(id + " " + user + " " + password);
		}
		// 7.关闭资源（后定义，先关闭）
		rs.close();
		stmt.close();
		conn.close();
	}
}
```
