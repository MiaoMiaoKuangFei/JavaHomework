# 一、这次练习中解决的问题
## 1. 配置环境
这个maven是只有专业版自带的，所以一开始的community是不行的。
## 2.maven的pom.xml
一开始这个文件是全部刷红的，最后才发现得让它Build里面Sync进行自己安装包。
## 3。解决level5不被兼容
    Intellij idea 报错：Error : java 不支持发行版本5
参考网站[Intellij idea 报错：Error : java 不支持发行版本5
](https://blog.csdn.net/qq_22076345/article/details/82392236)
## 4.使用自动化工具补全getter和setter
在右键加`generate`选项。
##5. @Autowired.
前者，Spring会直接将UserDao类型的唯一一个bean赋值给userDao这个成员变量；后者，Spring会调用setUserDao方法来将UserDao类型的唯一一个bean装配到userDao这个属性。
Spring 2.5 引入了 @Autowired 注释，它可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作。 通过 @Autowired的使用来消除 set ，get方法。

##6.Invalid bean definition with name 'dataSource' defined in class path resource [spring-mybatis.xml]:
    在对应的配置文件中没有把变量名正确的对应上
##7.不允许有匹配 "[xX][mM][lL]" 的处理指令目标
`<?xml version="1.0" encoding="UTF-8"?>`
必须放在.xml文件的第一行最开头的位置！

##8.元素类型为 "mapper" 的内容必须匹配 "(cache-ref|cache|resultMap*|parameterMap*|sql*|insert*|update*|delete*|select
删掉mapper里面的不规范表述，要把空格换行都删了就解决了
 
 ##9.Invalid bound statement (not found)
 主要是由于sql的xml文件中的名称和Dao类中不同，所以报错
 ##10. Autowiring: expected at least 1 bean which qualifies as autowire candidate for this dependency
 搞了我一晚上，心态崩了，其实在每个Service类前面加上@Service就行

 ##11.学会使用live-template
 自定义idea代码模板
 
 ##12.注意
 pojo层不能调用dao层
 
 ##13.一个或多个filter没有部署好
 又一个令人心态爆炸的问题\
 原因是external libraries里有包没有进到WEB-INF/lib里面\
 方法是File->ProjectStructure->artifacts里在Web/WEB-INFO/lib里添加没有的包
 
 
 ##14.404找不到资源
    <%--<%--%>
      <%--    pageContext.setAttribute("path", request.getContextPath());--%>
      <%--%>--%>
  因为这个东西一开始没有写controller也没有配好，所以用这个自然会404
  另外jsp一定要不能放在WEB-INF下
  
  ##15. 由没法注入产生的错误
  解决第一步，把mvc配置文件下改成
  
      <!-- 4.扫描web相关的bean -->
      <context:component-scan base-package="com.controller" />
      <context:component-scan base-package="com.service" />
      <context:component-scan base-package="com.dao" />
      
   解决第二步，把配置文件写成
   
       <init-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>classpath:spring/*.xml</param-value>
         </init-param>
   
   
   
之前用的是下面的配置方法，无论写进去dao还是mvc都会存在配不上的问题，所以都扫进去
    
     <param-value>classpath:spring/spring-dao.xml</param-value>       