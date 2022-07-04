import java.util.*;
import java.sql.*;
class Employee
{
	
	static void insert()
	{
		try
		 {
			Class.forName("com.mysql.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/employee","root","Password123");
			PreparedStatement stmt=con.prepareStatement("insert into EMP1 values(?,?,?,?,?)");
			Scanner sc=new Scanner(System.in);
			
			System.out.print("Enter Employee Id :");
			int id=sc.nextInt();
			System.out.print("Enter Employee Name :");  
			String name=sc.next();
			System.out.print("Enter Employee Age :");
		    int age=sc.nextInt();
			System.out.print("Enter Employee Salary :");
			int sal=sc.nextInt();
			System.out.print("Enter Employee Designation :");
			String desig=sc.next();
		
		stmt.setInt(1, id);
		stmt.setString(2,name);
		stmt.setInt(3,age);
		stmt.setInt(4,sal);
		stmt.setString(5, desig);
		stmt.execute();
		con.close();
		System.out.println("Data inserted successfully...");
		
		
		
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
	 }
		
		
	static void display()
	{
		try
		{
			Class.forName("com.mysql.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/employee","root","Password123");
			Statement stmt=con.createStatement();
			ResultSet rs=stmt.executeQuery("select * from EMP1");
			while(rs.next())
			{
				System.out.println(rs.getInt(1)+ ": "+rs.getString(2)+": "+rs.getInt(3)+" : "+rs.getInt(4)+" : "+rs.getString(5));
			}
		}
		catch (Exception e)
		{
		System.out.println(e);
		}
	
	}
	static void update()
	{
		try
		{
			Class.forName("com.mysql.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/employee","root","Password123");
			PreparedStatement  stmt=con.prepareStatement("update  EMP1 set salary=? where id=?");
			Scanner sc=new Scanner(System.in);
			
			System.out.print("Enter Employee Id :");
			int id=sc.nextInt();
			
			System.out.print("Enter Employee salary :");
			int salary=sc.nextInt();
			
			stmt.setInt(1, salary);
			stmt.setInt(2, id);
			
			stmt.execute();
			con.close();
			System.out.println("Data updated");
		}
			catch (Exception e)
			{
			System.out.println(e);
			}
				
			
	}
		
		
	
	static void delete()
	{
		try
		{
			Class.forName("com.mysql.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/employee","root","Password123");
			PreparedStatement stmt=con.prepareStatement("delete from EMP1 where id=?");
			Scanner sc=new Scanner(System.in);
			
			System.out.print("Enter Employee Id :");
			int id=sc.nextInt();
			
			stmt.setInt(1, id);
			System.out.println("do you really want to delete ? yes / no");
			String ch = sc.next();
			if(ch.equalsIgnoreCase("yes"))
			{
			stmt.execute();
			System.out.println("Data deleted");
			}
			else
			{
			System.out.println("Not deleted");
			}
			con.close();
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
	}
}

public class Project
{
	public static void main(String[]args)
	{
		int ch1=0,ch2=0;
		do
		{
			System.out.println("1). Insert");
			System.out.println("2). Dispaly");
			System.out.println("3). Update");
			System.out.println("4). Delete");
			System.out.println("5). EXit");
			System.out.println("Choose an option?");
			Scanner sc=new Scanner(System.in);
			ch1=sc.nextInt();
			if(ch1==1)
			{
				Employee.insert();
			}
			if(ch1==2)
			{
				Employee.display();
			}
			if(ch1==3) 
			{
				Employee.update();
			}
			if(ch1==4)
			{
				Employee.delete();
				
			}
		}
			while(ch1!=5);
		
	}
}