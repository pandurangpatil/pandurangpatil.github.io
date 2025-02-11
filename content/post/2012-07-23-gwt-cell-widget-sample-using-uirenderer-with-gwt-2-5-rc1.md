+++
title = "GWT Cell Widget sample using UiRenderer with GWT 2.5-RC1"
slug = "2012-07-23-gwt-cell-widget-sample-using-uirenderer-with-gwt-2-5-rc1"
published = 2012-07-23T20:43:00.004000-07:00
author = "Pandurang Patil"
tags = [ "GWT", "UiRenderer", "CellWidget",]
+++
**GWT Cell Widget sample using UiRenderer.**
  
  
I tried this sample with GWT 2.5 RC1 release. For official documentation [refer](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiBinder#Rendering_HTML_for_Cells). Below sample is simple sample which will display contents of Person entity using custom cell. And such list of entities can be displayed with cell list.  
  
`Person.java`

     public class Person {  
       private String  fname;  
       private String  lname;  
       private String  emailid;  
       private int    age;  
       /**  
        * @return the fname  
        */  
       public String getFname() {  
         return fname;  
       }  
       /**  
        * @param fname  
        *      the fname to set  
        */  
       public void setFname(String fname) {  
         this.fname = fname;ravi.kumar@gmail.com   
       }  
       /**  
        * @return the lname  
        */  
       public String getLname() {  
         return lname;  
       }  
       /**  
        * @param lname  
        *      the lname to set  
        */  
       public void setLname(String lname) {  
         this.lname = lname;  
       }  
       /**  
        * @return the emailid  
        */  
       public String getEmailid() {  
         return emailid;  
       }  
       /**  
        * @param emailid  
        *      the emailid to set  
        */  
       public void setEmailid(String emailid) {  
         this.emailid = emailid;  
       }  
       /**  
        * @return the age  
        */  
       public int getAge() {  
         return age;  
       }  
       /**  
        * @param age  
        *      the age to set  
        */  
       public void setAge(int age) {  
         this.age = age;  
       }  
     }  

  
`PersonCell.ui.xml`  
  

     <ui:UiBinder xmlns:ui='urn:ui:com.google.gwt.uibinder'>  
       <ui:with field='person' />  
       <div>  
         First Name :  
         <span>  
           <ui:text from='{person.getFname}' />  
         </span>  
         <p>  
           Last Name :  
           <span>  
             <ui:text from='{person.getLname}' />  
           </span>  
         </p>  
         <p>  
           Email :  
           <span>  
             <ui:text from='{person.getEmailid}' />  
           </span>  
         </p>  
       </div>  
     </ui:UiBinder>  

  

`PersonCell.java`  
  

     public class PearsonCell extends AbstractCell<Person> {  
       interface MyUiRenderer extends UiRenderer {  
         void render(SafeHtmlBuilder sb, Person person);  
       }  
       private static MyUiRenderer  renderer  = GWT.create(MyUiRenderer.class);  
       @Override  
       public void render(com.google.gwt.cell.client.Cell.Context context, Person value, SafeHtmlBuilder sb) {  
         renderer.render(sb, value);  
       }  
     }  

  
Using above created `PersonCell`  
  

         PersonCell cell = new PersonCell();  
         CellList<Person> cellList = new CellList<Person>(cell);  
         List<Person> list = new ArrayList<Person>();  
         Person p = new Person();  
         p.setFname("Pranoti");  
         p.setLname("Patil");  
         p.setEmailid("pra.....@gmail.com");  
         p.setAge(30);  
         list.add(p);  
         p = new Person();  
         p.setFname("Pandurang");  
         p.setLname("Patil");  
         p.setEmailid("pa.....@gmail.com");  
         p.setAge(30);  
         list.add(p);  
         p = new Person();  
         p.setFname("Ravi");  
         p.setLname("Kumar");  
         p.setEmailid("ra.....@gmail.com");  
         p.setAge(30);  
         list.add(p);  
         cellList.setRowCount(list.size(), true);  
         cellList.setRowData(list);  
         RootPanel.get().add(cellList);   

  
Out put of above sample :  
  

    First Name : Pranoti Last Name : Patil  
    Email :.......................@gmail.com

    First Name : Pandurang Last Name : Patil  
    Email : .......................@gmail.com

    First Name : Ravi Last Name : Kumar  
    Email : .......................@gmail.com  
  
  
[Refer](https://groups.google.com/forum/#%21searchin/google-web-toolkit/uirenderer/google-web-toolkit/TWYcWRfICXk/c421BfbJvhAJ) discussion.
