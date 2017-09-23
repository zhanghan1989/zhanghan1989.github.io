---
title: salesforce_基础_001_Apex初级
categories: salesforce
tags: salesforce
photos:
- /images/salesforce.jpeg
---


## Apex - 数据类型

原始数据类型：Integer, Double, Long, Date, Datetime, String, ID, Boolean)

String

集合：Lists, Sets, Maps 

sObject通用类型

Enums(枚举)

Classes, Objects and Interfaces (类，对象和接口)


Integer: 32位数，值的范围是-2,147,483,648，最大值为2,147,483,647（2^31-1）。
Integer barrelNumbers = 1000;
system.debug(' value of barrelNumbers variable: '+barrelNumbers);

Long: 64位数
Long companyRevenue  = 21474838973344648L;
system.debug('companyRevenue'+companyRevenue);

Boolean:
Boolean shipmentDispatched;
shipmentDispatched = true;
System.debug('Value of shipmentDispatched '+shipmentDispatched);

Date:
Date ShipmentDate = date.today();
System.debug('ShipmentDate '+ShipmentDate);

String:
String companyName = 'Abc International';
System.debug('Value companyName variable'+companyName);


Object: 对象
Account objAccount = new Account (Name = 'Test Chemical');
system.debug('Account value'+objAccount);
MyApexClass  classObj = new MyApexClass();


sObject: Salesforce中的特殊数据类型
有两种类型的sObjects：Standard和Custom。
Account objAccount = new Account();
objAccount.Name = 'ABC Customer';
objAccount.Description = 'Test Account';
System.debug('objAccount variable value'+objAccount);

APEX_Customer_c objCustomer = new APEX_Customer_c();
objCustomer.APEX_Customer_Decscription_c = 'Test Customer';
System.debug('value objCustomer'+objCustomer);


Time:时间
此变量用于存储特定时间。 此变量应始终使用系统静态方法声明。
Blob:斑点
Blob是作为对象存储的二进制数据的集合。 当我们要将Salesforce中的附件存储到变量中时，将使用此选项。 此数据类型转换单个对象中的附件。 当我们需要将blob转换为字符串时，我们可以使用toString和valueOf方法在需要时将其转换为字符串。
Enum:枚举
枚举是一种抽象数据类型，存储指定标识符的有限集合的一个值。
可以使用关键字Enum定义一个枚举。 枚举可用作Salesforce中的任何其他数据类型。
public enum Compounds {HCL, H2SO4, NACL, HG}

Compounds objC = Compounds.HCL;
System.debug('objC value: '+objC);

===================================================

## Apex - 变量

声明局部变量:
String productName = 'HCL';
Integer i=0;
Set<string> setOfProducts = new Set<string>();
Map<id, string> mapOfProductIdToName = new Map<id, string>();

Integer默认为null
变量不区分大小写

===================================================

## Apex - 常量
```apex
public class CustomerOperationClass {
    static final Double regularCustomerDiscount = 0.1;
    static Double finalPrice = 0;
    public static Double provideDiscount (Integer price) {
        //calculate the discount
        finalPrice = price - price*regularCustomerDiscount;
        return finalPrice;
    }
}

Double finalPrice = CustomerOperationClass.provideDiscount(100);
```
===================================================

## Apex - 字符串

### contains：包含
String myProductName1 = 'HCL';
String myProductName2 = 'NAHCL';
Boolean result = myProductName2.contains(myProductName1);

### equals：字符串具有相同的二进制字符序列，并且它们不为空。区分大小写。
String myString1 = 'MyString';
String myString2 = 'MyString';
Boolean result = myString2.equals(myString1);

### equalsIgnoreCase：不区分大小写。
String myString1 = 'MySTRING';
String myString2 = 'MyString';
Boolean result = myString2.equalsIgnoreCase(myString1);

### emove：从给定字符串中删除提供的字符串
String myString1 = 'This Is MyString Example';
String stringToRemove = 'MyString';
String result = myString1.remove(stringToRemove);

### removeEndIgnoreCase：删除中从给定字符串中提取的字符串。前提是它出现在结尾。 不区分大小写。
String myString1 = 'This Is MyString EXAMPLE';
String stringToRemove = 'Example';
String result = myString1.removeEndIgnoreCase(stringToRemove);

### startWith：判断给定的字符串是否是方法中提供的前缀开头
String myString1 = 'This Is MyString EXAMPLE';
String prefix = 'This';
Boolean result = myString1.startsWith(prefix);

===================================================

## Apex - 数组

//Defining array
String [] arrayOfProducts = new List<String>();
//Adding elements in Array
arrayOfProducts.add('HCL');
arrayOfProducts.add('H2SO4');
arrayOfProducts.add('NACL');
arrayOfProducts.add('H2O');
arrayOfProducts.add('N2');
arrayOfProducts.add('U296');

for (Integer i = 0; i<arrayOfProducts.size(); i++) {
    //This loop will print all the elements in array
    system.debug('Values In Array: '+arrayOfProducts[i]);   
}

===================================================

## Apex - 集合

### Lists 列表
List<string> ListOfCities = new List<string>();
String [] ListOfStates = new List<string>();
初始值：List<string> ListOfStates = new List<string> {'NY', 'LA', 'LV'}();

字符串：
List<string> ListOfCities = new List<string>();
String [] ListOfStates = new List<string>();
初始值：List<string> ListOfStates = new List<string> {'NY', 'LA', 'LV'}();

sObject：
List<account> AccountToDelete = new List<account> ();

嵌套List：
List<List<Set<Integer>>> myNestedList = new List<List<Set<Integer>>>();

方法：
size()，add()，get()，clear()，set()
List<string> ListOfStatesMethod = new List<string>();
ListOfStatesMethod.add('New York');
String StateAtFirstPosition = ListOfStatesMethod.get(0);
ListOfStatesMethod.set(0, 'LA');
ListOfStatesMethod.clear();


### Sets 无序集合

Set<string> ProductSet = new Set<string>{'Phenol', 'Benzene', 'H2SO4'};

方法：
Set<string> ProductSet = new Set<string>{'Phenol', 'Benzene', 'H2SO4'};
ProductSet.add('HCL');
ProductSet.remove('HCL');
ProductSet.contains('HCL');


### Maps （key区分大小写）

Map<string, string> ProductCodeToProductName = new Map<string, string> {'1000'=>'HCL', '1001'=>'H2SO4’};

方法：

Map<string, string> ProductCodeToProductName = new Map<string, string>(); 
ProductCodeToProductName.put('1002', 'Acetone');
ProductCodeToProductName.containsKey('1002')
String value = ProductCodeToProductName.get('1002'); 
Set SetOfKeys = ProductCodeToProductName.keySet();

===================================================

## Apex - 类


private | public | global 
[virtual | abstract | with sharing | without sharing] 
class ClassName [implements InterfaceNameList] [extends ClassName] 
{ 
// Classs Body
}

public class MySampleApexClass {
    public static Integer myValue = 0;
    public static String myString = '';
    
    public static Integer getCalculatedValue () {
            myValue = myValue+10;
            return myValue;
    }
}
访问修饰符

Private：如果您将访问修饰符声明为“私有”，则此类将仅在本地已知，并且您无法在该特定片段之外访问此类。 默认情况下，类有此修饰符。
Public：如果你声明该类为“公共”，这意味着这个类是可访问您的组织和您定义的命名空间。 通常，大多数Apex类都使用此关键字定义。
Global：如果将类声明为“全局”，那么无论您的组织如何，都可以由所有顶点代码访问。 如果您使用webservice关键字定义方法，那么必须使用global关键字声明包含类。



共享模式

共享：这是Salesforce中的Apex类的一个特殊功能。当使用“With Sharing”关键字指定类时，它具有以下含义：当类将被执行时，它将尊重用户的访问设置和配置文件权限。假设，用户的操作已经触发了30条记录的记录更新，但用户只能访问20条记录，并且不能访问10条记录。然后，如果类正在执行更新记录的操作，则只有20个记录将被更新，用户有权访问，其余10个记录不会更新。这也称为用户模式

无共享：即使用户无法访问30个中的10个记录，所有30个记录也将随着类在系统模式下运行而更新，即它已使用无共享关键字定义。这称为系统模式。

虚拟：如果你使用'virtual'关键字，那么它表示这个类可以被扩展并允许覆盖。如果你想覆盖方法，那么类应该使用virtual关键字声明。

抽象：如果你声明该类为'abstract'，那么它将只包含方法的签名，而不是实际的实现。



类变量

[public | private | protected | global] [final] [static] data_type variable_name [= value]
* 变量数据类型和变量名称是必需的
* 访问修饰符和值是可选的。

public static final Integer myvalue

类方法


[public | private | protected | global] 
[override] 
[static] 
return_data_type method_name (input parameters) 
{
// Method body goes here
}
public: 将可以从类中的任何地方和类之外访问。 
private: 只能在类中访问。 
global: 将被所有Apex类访问，并且可以作为其他顶点类访问的Web服务方法。


类构造函数
默认情况下调用无参数构造函数。
使用例：当调用类时，您想要将某些整数变量的值赋值为0。

重载构造函数
构造函数可以重载，即一个类可以有不止一个用不同参数定义的构造函数。

public MySampleApexClass3 () {
    myValue = 100;  //initialized variable when class is called
    System.debug('myValue  variable with no Overaloading'+myValue);
}
    
public MySampleApexClass3 (Integer newPrice) {  //Overloaded constructor
    myValue = newPrice; //initialized variable when class is called
    System.debug('myValue  variable with Overaloading'+myValue);
}

===================================================

## Apex - 对象

类的实例称为对象。就Salesforce而言，对象可以是类，也可以创建sObject的对象。

### 从类创建对象：

类：
public class MyClass {
    Integer myInteger = 10;
    public void myMethod (Integer multiplier) {
        Integer multiplicationResult;
        multiplicationResult=multiplier*myInteger;
        System.debug('Multiplication is '+multiplicationResult);
    }
}

对象：
MyClass objClass = new MyClass();
objClass.myMethod(100);


### sObject创建：

Account objAccount = new Account();
objAccount.Name = 'Testr Account';

APEX_Customer_c objCustomer = new APEX_Customer_c ();
objCustomer.Name = 'ABC Customer';



静态初始化：

当加载类时，静态方法和变量只初始化一次。 静态变量不会作为Visualforce页面的视图状态的一部分传输。

===================================================

## Apex - 接口

方法只有声明，没有实现。
实现接口，就要强制实现该接口的方法。
接口主要用于为代码提供抽象层。

public interface DiscountProcessor{
    Double percentageDiscountTobeApplied();
}

public class PremiumCustomer implements DiscountProcessor{
    public Double percentageDiscountTobeApplied () {
            return 0.30;
    }
}

public class NormalCustomer implements DiscountProcessor{
    public Double percentageDiscountTobeApplied () {
            return 0.10;
    }
}

标准Salesforce接口：

例如，Database.Batchable，Schedulable等
如果实现Database.Batchable接口，那么必须实现接口中定义的三个方法：开始，执行和完成。

global class CustomerProessingBatch implements Database.Batchable<sobject>, Schedulable{
    //Add here your email address
    global String [] email = new String[] {'test@test.com'};
  
    //Start Method
    global Database.Querylocator start (Database.BatchableContext BC) {
    //This is the Query which will determine the scope of Records and fetching the same
    return Database.getQueryLocator('Select id, Name, APEX_Customer_Status__c, APEX_Customer_Decscription__c From APEX_Customer__c WHERE createdDate = today && APEX_Active__c = true');
}

//Execute method
global void execute (Database.BatchableContext BC, List<sobject> scope) {
    List<apex_customer__c> customerList = new List<apex_customer__c>();
    List<apex_customer__c> updtaedCustomerList = new List<apex_customer__c>();
    for (sObject objScope: scope) {
        //type casting from generic sOject to APEX_Customer__c
        APEX_Customer__c newObjScope = (APEX_Customer__c)objScope ;
        newObjScope.APEX_Customer_Decscription__c = 'Updated Via Batch Job';
        newObjScope.APEX_Customer_Status__c = 'Processed';
        //Add records to the List
        updtaedCustomerList.add(newObjScope);
    }       
    
    //Check if List is empty or not
    if (updtaedCustomerList != null && updtaedCustomerList.size()>0) {
            //Update the Records
        Database.update(updtaedCustomerList); System.debug('List Size '+updtaedCustomerList.size());
    }
}

    //Finish Method
    global void finish(Database.BatchableContext BC){
    Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
   
    //get the job Id
    AsyncApexJob a = [Select a.TotalJobItems, a.Status, a.NumberOfErrors, a.JobType, a.JobItemsProcessed, a.ExtendedStatus, a.CreatedById, a.CompletedDate From AsyncApexJob a WHERE id = :BC.getJobId()];
    System.debug('$$$ Jobid is'+BC.getJobId());
    
    //below code will send an email to User about the status
    mail.setToAddresses(email);
    
    //Add here your email address
    mail.setReplyTo('test@test.com');
    mail.setSenderDisplayName('Apex Batch Processing Module');
    mail.setSubject('Batch Processing '+a.Status);
    mail.setPlainTextBody('The Batch Apex job processed  '+a.TotalJobItems+'batches with  '+a.NumberOfErrors+'failures'+'Job Item processed are'+a.JobItemsProcessed);
  
    Messaging.sendEmail(new Messaging.Singleemailmessage [] {mail});
}

//Scheduler Method to scedule the class
    global void execute(SchedulableContext sc){
        CustomerProessingBatch conInstance = new CustomerProessingBatch();
        database.executebatch(conInstance,100);
    }
}

CustomerProessingBatch objBatch = new CustomerProessingBatch ();
Database.executeBatch(objBatch);