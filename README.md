# belajar-spring-boot

Building Simple Java Application with Spring Boot.
<br/><br/>
IDE used: Eclipse 
1.	Maven Project Web Application: File -> New -> Project ->  Maven Project
2.	Pilih workspace, pilih archetype maven webapp, isi group-id dan artifact-id. Contoh: 
    group-id: com.putra,
    artifact-id: belajar.
    Lalu finish
3.	Setelah project terbentuk, jika terjadi error kemungkinan terjadi masalah pada runtime, klik kanan pada project -> Properties -> Project Facet -> Runtimes -> New -> Pilih Server misalnya Apache Tomcat v8.0
4.	Pom.xml
```
  <parent>
    <groupId>org.springframework.boot</groupId>
	  <artifactId>spring-boot-starter-parent</artifactId>
	  <version>2.1.1.RELEASE</version>
  </parent>

  <properties>
	  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<!-- Spring Boot -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<!-- Tomcat Embed -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
		
		<!-- JSTL -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
		</dependency>
	</dependencies>
	<build>
		<finalName>belajar-maven</finalName>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
```
5.	Update project: klik kanan project -> Maven -> Update Project..
6.	Buat folder java di src/main, lalu refresh 
7.	Di src/main/java buat package com.belajar.app 
8.	Di dalam com.belajar.app buat kelas Application.java sebagai main class
```
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.boot.builder.SpringApplicationBuilder;
  import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;
  import org.springframework.context.annotation.ComponentScan;
  @SpringBootApplication
  @ComponentScan(basePackages={"com.belajar.controller"})
  public class Application extends SpringBootServletInitializer {

    @Override
      protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        	return application.sources(Application.class);
    	}

    	public static void main(String[] args) {
        	SpringApplication.run(Application.class, args);
    	}
}
```
9.	Buat package com.belajar.controller 
10.	Di dalam com.belajar.controller buat kelas HomeController.java
```
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HomeController {
    @GetMapping({"/", "/hello"})
    public String hello(Model model, @RequestParam(value="name", required=false, defaultValue="World") String name) {
        	model.addAttribute("name", name);
        	return "hello";
    }
}
```
18.	hello.jsp di WEB-INF/jsp/
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello ${name}!</title>
    <link href="/css/main.css" rel="stylesheet">
</head>
<body>
    <h2 class="hello-title">Hello ${name}!</h2>
    <script src="/js/main.js"></script>
</body>
</html>
```
19.	Di resources buat application.properties
```
spring.mvc.view.prefix: /WEB-INF/jsp/
spring.mvc.view.suffix: .jsp

## Embedded Server Configuration
server.port = 8091
```
11.	Run project dengan klik kanan project -> Run as -> Maven Build.. <br/> Pada goals isi: spring-boot:run
12.	Jika terjadi error “No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?”, cara solve: Window -> Preferences -> Java -> installed JREs -> Execution Environment -> Pilih salah satu misal: JavaSE-1.8
13.	Buka localhost:8091 di web browser
