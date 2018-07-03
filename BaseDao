package com.dao.impl;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

/**
 * 操作数据库的工具类
 * 
 * @author 王建兵 @version1.0
 */
public class BaseDao {
	// 定义连数据库的参数
	private final String driverClass = "com.mysql.jdbc.Driver";
	private final String url = "jdbc:mysql://localhost:****/mydatabase";
	private final String username = "****";
	private final String password = "****";

	private Connection con = null;
	private PreparedStatement ps = null;
	private ResultSet rs = null;

	/**
	 * 获取jdbc的连接对象
	 * 
	 * @return 连接对象
	 */
	public Connection getConn() {
		try {
			Class.forName(this.driverClass);
			this.con = DriverManager.getConnection(this.url, this.username, this.password);
			return this.con;
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return null;
	}

	/**
	 * 执行添加，修改，删除语句 语句采用的预执行对象支持参数化sql 返回影响行数
	 * 
	 * @param sql
	 *            sql语句，支持参数化
	 * @param params
	 *            参数值，无参传null
	 * @return 影响行数
	 */
	public int executeUpdate(String sql, Object[] params) {
		int temp = -1;
		try {
			this.getConn(); // 获取连接对象
			ps = con.prepareStatement(sql); // 预执行对象
			if (params != null) {
				for (int i = 0; i < params.length; i++) {
					ps.setObject(i + 1, params[i]);
				}
			}
			temp = ps.executeUpdate(); // 执行
		} catch (SQLException e) {
			e.printStackTrace();
		} finally {
			this.closeAll();
		}
		return temp;
	}

	/**
	 * 执行查询 返回结果集
	 * 
	 * @param selectsql
	 *            查询语句支持参数
	 * @param params
	 *            参数
	 * @return 结果集
	 */
	public ResultSet executeQuery(String selectsql, Object[] params) {
		try {
			this.getConn(); // 获取连接对象
			ps = con.prepareStatement(selectsql); // 预执行对象
			if (params != null) {
				for (int i = 0; i < params.length; i++) {
					ps.setObject(i + 1, params[i]);
				}
			}
			rs = ps.executeQuery(); // 执行
			return rs;
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return null;
	}

	// 关闭资源方法
	public void closeAll() {
		try {
			if (rs != null) {
				rs.close();
				rs = null;
			}
			if (ps != null) {
				ps.close();
				ps = null;
			}
			if (con != null) {
				con.close();
				con = null;
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
