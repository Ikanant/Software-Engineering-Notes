Introduction

Sunday, February 10, 2019

11:04 AM

 

The Spring framework started out as an inversion of controls framework. It was conceived to reduce the tedious configuration required to setup earlier JAVA Enterprise Edition development. Spring was later built around using JAVA without EJBs (Enterprise JavaBeans)

 

Spring enabled us to do enterprise development without the use of an application server. TOMCAT is NOT an application server, it\'s just a web-server. Tomcat is simple to use and compared to other enterprise options it\'s a lot more lightweight.

 

Spring is completely POJO (Plain Java Old Java Object) based.

 

Spring uses AOPs / Proxies to apply things like transactions to our code.

 

![JEE POJO Based Unobtrusive AOP/Proxies Best Practices ](000_Introduction_000.png)

 

 

What does SPRING helps us with?\
 

-   Testability

-   Maintainability

-   Scalability

-   Reduce Complexity

-   Put\'s the focus on the business\
     

![Business FOCUS public Car getById(String id) { Connection con = null; PreparedStatement stmt = null; ResultSet rs = null; try { String sql = \"select \* from CAR where ID = con = DriverMa etConnection \"l stmt = con .prepareStatement sq stmt. setString(1, id); rs = stmt. executeQuery(); if(rs. next()) { car. setMake(rs. getString( return car; else { return null; } catch (SQLException e) { e.printStackTrace();} finally { try { if(rs null && { rs.close(); } catch (Exception e) {Y return null; : 33Ø6/cars \" ) ; ](000_Introduction_001.png)

\^\^\^ Lots of junk for configuration

 

 

![public Car getById(String id) { Connection con = null; PreparedStatement stmt = null; ResultSet rs = null; try { String sql = \"select \* from CAR where ID = ?\"; con = DriverManager 33Ø6/cars \" ) ; stmt = con.prepareStatement(sql); stmt. setString(1, id); rs = stmt. executeQuery(); Car car new Car(); car. . getString(1)) ; return car; else { return null; } catch (SQLException e) { e.printStackTrace();} finally { try { if(rs null && { rs.close(); } catch (Exception e) return null; public Car findCar(String id) { return Id) ](000_Introduction_002.png)

 

 

**How does everything works then?\
** 

As we said before, everything in SPRING can be broken down to a single POJO. SPRING itself can even be considered a glorified HashMap (it\'s doing way more than that but we can think of it that way). Spring can be used as a Registry (basic demo I have on Github)...

 

The image bellow is what a Spring container would look like if we crafted it all out. One of these beans might be a statement, one of them might be a \'prepare\' statement, one of them might be a connection behind the scenes, an entity manager. All of beans are stored in these containers and that\'s when the HashMap analogy comes into place.

 

![雀로口투口毒 ](000_Introduction_003.png)

 
