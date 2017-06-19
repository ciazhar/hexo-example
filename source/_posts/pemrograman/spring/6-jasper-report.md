---
title: Membuat Report dengan Jasper Report
date: 2017-04-23 14:17:39
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)

1. Tambahkan dependency
```xml
<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context-support</artifactId>
		</dependency>
		<dependency>
			<groupId>io.github.jpenren</groupId>
			<artifactId>thymeleaf-spring-data-dialect</artifactId>
			<version>2.1.1</version>
		</dependency>
		<dependency>
			<groupId>net.sf.jasperreports</groupId>
			<artifactId>jasperreports</artifactId>
			<version>6.3.1</version>
		</dependency>
		<dependency>
			<groupId>org.apache.poi</groupId>
			<artifactId>poi</artifactId>
			<version>3.10.1</version>
		</dependency>
```
1. Membuat file .jrxml menggunakan Jaspersoft Studio
2. Copy file ke resource/reports
3. tambahkan bean `JasperReportsViewResolver` ke konfigurasiweb
```java
@Bean
    public JasperReportsViewResolver getJasperReportsViewResolver(){
        JasperReportsViewResolver resolver = new JasperReportsViewResolver();
        resolver.setPrefix("classpath:/reports/");
        resolver.setSuffix(".jrxml");
        resolver.setViewNames("report_*");
        resolver.setViewClass(JasperReportsMultiFormatView.class);
        resolver.setOrder(0);
        return resolver;
    }
```
- buat controllernya
```java
@Controller
public class BugReportController {
    @Autowired private BugDao dao;

    @RequestMapping("/bug")
    public ModelAndView generateAllBugReport(ModelAndView m,
                                             @RequestParam(value = "format", required = false) String format){
        Iterable<Bug> data = dao.findAll();
        m.addObject("dataSource", data);
        m.addObject("tanggalUpdate", new Date());
        m.addObject("format", "pdf");

        if(format != null && !format.isEmpty()){
            m.addObject("format", format);
        }

        m.setViewName("report_bug");
        return m;
    }
}
```
