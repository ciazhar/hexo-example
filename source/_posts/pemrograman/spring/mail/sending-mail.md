---
title: Sending Mail + Verifikasi Email
date: 2017-08-17 07:40:10
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)

# Sending Email
- Tambahkan Dependency `Spring Boot Mail`
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```
- Konfigurasi Mail Server
```yml
# Mail Configuration
  mail:
    host: smtp.gmail.com
    port: 587
    username: email@gmail.com   #ini nama email
    password: pass              #ini password email
    properties:
      mail:
        smtp:
          starttls:
            enabled: true
            required: true
          auth: true
          connectiontimeout: 5000
          timemout: 5000
          writetimeout: 5000
```
- Membuat Model Email.
```java
public class EmailStatus{
    public static final String SUCCESS = "SUCCESS";
    public static final String ERROR = "ERROR";
 
    private final String to;
    private final String subject;
    private final String body;
 
    private String status;
    private String errorMessage;
 
    public EmailStatus(String to, String subject, String body) {
        this.to = to;
        this.subject = subject;
        this.body = body;
    }
 
    public EmailStatus success() {
        this.status = SUCCESS;
        return this;
    }
 
    public EmailStatus error(String errorMessage) {
        this.status = ERROR;
        this.errorMessage = errorMessage;
        return this;
    }
 
    public boolean isSuccess() {
        return SUCCESS.equals(this.status);
    }
 
    public boolean isError() {
        return ERROR.equals(this.status);
    }
 
    public String getTo() {
        return to;
    }
 
    public String getSubject() {
        return subject;
    }
 
    public String getBody() {
        return body;
    }
 
    public String getStatus() {
        return status;
    }
 
    public String getErrorMessage() {
        return errorMessage;
    }
}
```
- Membuat component untuk send email
```java
@Component
public class EmailSender{
    @Autowired 
    JavaMailSender javaMailSender;

    Logger logger = LoggerFactory.getLogger(this.getClass());
	
	public EmailStatus sendPlainText(String to, String subject, String text) {
        return sendM(to, subject, text, false);
    }
 
    public EmailStatus sendHtml(String to, String subject, String htmlBody) {
        return sendM(to, subject, htmlBody, true);
    }
 
    private EmailStatus sendM(String to, String subject, String text, Boolean isHtml) {
        try {
            MimeMessage mail = javaMailSender.createMimeMessage();
            MimeMessageHelper helper = new MimeMessageHelper(mail, true);
            helper.setTo(to);
            helper.setSubject(subject);
            helper.setText(text, isHtml);
            javaMailSender.send(mail);
            logger.info("Send email '{}' to: {}", subject, to);
            return new EmailStatus(to, subject, text).success();
        } catch (Exception e) {
            logger.error(String.format("Problem with sending email to: {}, error message: {}", to, e.getMessage()));
            return new EmailStatus(to, subject, text).error(e.getMessage());
        }
    }
}
```
- Membuat component
```java
@Component
public class EmailHtmlSender{
    @Autowired private EmailSender mailSender;

    @Autowired private TemplateEngine templateEngine;

    public EmailStatus send(String to, String subject, String templateName, Context context) {
        String body = templateEngine.process(templateName, context);
        return mailSender.sendHtml(to, subject, body);
    }
}
```
- Membuat html
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title th:remove="all">Order Confirmation</title>
</head>
<body>
<div>
     
        <h2 th:text="${title}">title</h2>
        <p th:text="${description}"></p>
         <p>
            <a th:href="@{http://localhost:8080/activate(email=${email})}">Verification Link</a>
        </p>      
</div>
 
</body>
</html>
```
- Membuat service
```java
public interface EmailService{

    EmailStatus sendEmail(RegisterForm form);
}
```
- Membuat service impl
```java
@Service
public class EmailServiceImpl implements EmailService{

    @Autowired
	public EmailHtmlSender emailHtmlSender;

    @Override
    public EmailStatus sendEmail(RegisterForm form){
        Context context = new Context();
        context.setVariable("title", "Clorus Email Verification");
        context.setVariable("description", "To Verify your clorus account please click link below ");
        context.setVariable("email",form.getEmail());
        
        EmailStatus emailStatus = emailHtmlSender.send(form.getEmail(), "Clorus Email Verification", "mail", context);

        return emailStatus;
    }
}
```
- Membuat controller
```java
@PreAuthorize("permitAll()")
    @RequestMapping(method = RequestMethod.POST,value = "/register")
    public ResponseData<Object> register(@RequestBody @Valid RegisterForm form)throws Exception{
        ResponseData<Object> responseData = new ResponseData<>();
        userService.register(form);
        responseData.setData(emailService.sendEmail(form));
        return responseData;
    }
```

# Verifikasi Email
- Membuat controller
```java
public class UserThymeleafController{

    @Autowired private UserRepository userRepository;


    @PreAuthorize("permitAll()")
    @RequestMapping("/activate")
    public String activate (@RequestParam (value="email")String email,Model model){
        User user = userRepository.findByEmail(email);
        model.addAttribute("email",user.getEmail());

        Logger logger = LoggerFactory.getLogger(this.getClass());
        logger.info("\n\n Email yang dikirim yaitu\n\n\n", user.getEmail());

        user.setEnabled(true);
        userRepository.save(user);
        
        return "/activate";
    }

}
```

- Membuat html
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title >Aktivasi Akun</title>
</head>
<body>
<div>
    <p>Selamat <span th:text="${email}"></span>, anda telah berhasil melakukan aktivasi akun. Silahkan nikmati layanan kami.</p>
</div>
 
</body>
</html>
```