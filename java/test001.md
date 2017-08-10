# java常量池

```
package com.jvm.test;

/**
 * Created by wangkai on 2017/8/4.
 */
public class StringIntern {
    /**
     * intern()方法设计的初衷，就是重用String对象，以节省内存消耗。
     * jdk1.7以上
     */

    public void test(){
        System.out.println("--------test-------");
        String str = new String("abc");     //在常量池中创建字符串"abc",在堆中创建引用名为str对象
        System.out.println("str.intern()==str : " + (str.intern()==str));
        //str.intern() 将"abc"放入常量池中,因为"abc"已经在常量池中,所以str.intern()不起作用

        //str.intern()==str : false
        //常量池地址 和 堆地址 不同
    }

    public void test1(){
        System.out.println("--------test1-------");
        String str = "abc1";    //在常量池中创建字符串"abc1"
        String str1 = new String("abc1");   //在堆中创建引用名为str1对象,"abc1"已经在常量中

        System.out.print("str == str1 : ");
        System.out.println(str == str1);    //str == str1 : false

        System.out.print("str == str1.intern() : ");
        System.out.println(str == str1.intern());   //str == str1.intern() : true

    }

    public void test2(){
        System.out.println("--------test2-------");
        String str = "abc2";
        String str1 = new String("abc2");
        String str2 = str1.intern();

        System.out.print("str == str1 : ");
        System.out.println(str == str1);    //str == str1 : false

        System.out.print("str == str2 : ");
        System.out.println(str == str2);   //str == str2 : true
    }

    public void test3_0(){
        System.out.println("--------test3_0-------");
        String str1 = new String("ab3_0") + new String("c3_0");
        //在常量池中创建"ab3_0","c3_0",在堆中创建引用名为str1对象,此时常量池中并无"ab3_0c3_0"
        String str2 = "ab3_0c3_0";
        System.out.println("str1 : " + str1);
        System.out.println("str2 : " + str2);
        System.out.println("str1 == \"ab3_0c3_0\" : " + (str1 == "ab3_0c3_0"));
        System.out.println("str1 == str2 : " + (str1 == str2));

//        str1 : ab3_0c3_0
//        str2 : ab3_0c3_0
//        str1 == str2 : false
    }

    public void test3(){
        System.out.println("--------test3-------");
        String str1 = new String("ab3") + new String("c3");

        System.out.println("str1.intern() == str1 : " + (str1.intern() == str1));
        //jdk1.7以后,将常量池放入堆中,此时常量池中无"ab3c3",str1.intern()直接在常量池中存储str1对象
        System.out.println("str1 : " + str1);
        System.out.println("str1 == \"ab3c3\" : " + (str1 == "ab3c3"));
        System.out.println("str1.intern() == \"ab3c3\" : " + (str1.intern() == "ab3c3"));
        String str2 = "ab3c3";
        System.out.println("str1 == str2 : " + (str1 == str2));

//        str1.intern() == str1 : true
//        str1 : ab3c3
//        str1 == "ab3c3" : true
//        str1.intern() == "ab3c3" : true
//        str1 == str2 : true
    }

    public void test3_1(){
        System.out.println("--------test3_1-------");
        String str1 = new String("ab3_1") + new String("c3_1");
        if((str1 == "ab3_1c3_1")){
            System.out.println("yes");
        }
        System.out.println("str1.intern() == str1 : " + (str1.intern() == str1));
        System.out.println("str1.intern() == \"ab3_1c3_1\" : " + (str1.intern() == "ab3_1c3_1"));
        String str2 = "ab3_1c3_1";
        System.out.println("str1 == str2 : " + (str1 == str2));

//        str1.intern() == str1 : false
//        str1.intern() == "ab3_1c3_1" : true
//        str1 == str2 : false
    }

    public void test3_2(){
        System.out.println("--------test3_1-------");
        String str1 = new String("ab3_2") + new String("c3_2");
        if((str1 == "xxxx")){
            System.out.println("yes");
        }
        System.out.println("str1.intern() == str1 : " + (str1.intern() == str1));
        System.out.println("str1.intern() == \"ab3_2c3_2\" : " + (str1.intern() == "ab3_2c3_2"));
        String str2 = "ab3_2c3_2";
        System.out.println("str1 == str2 : " + (str1 == str2));

//        str1.intern() == str1 : true
//        str1.intern() == "ab3_1c3_1" : true
//        str1 == str2 : true
    }

    public void test4(){
        System.out.println("--------test4-------");
        String str = "ab4c4";
        String str1 = new String("ab4") + new String("c4");

        System.out.println("str1.intern() == str1 : " + (str1.intern() == str1));
        System.out.println("str1 : " + str1);
        System.out.println("str1 == \"ab4c4\" : " + (str1 == "ab4c4"));
        System.out.println("str1.intern() == \"ab4c4\" : " + (str1.intern() == "ab4c4"));

//        str1.intern() == str1 : false
//        str1 : ab4c4
//        str1 == "ab4c4" : false
//        str1.intern() == "ab4c4" : true

    }

    public static void main(String[] args){
        StringIntern s = new StringIntern();
        s.test();
        s.test1();
        s.test2();
        s.test3_0();
        s.test3();
        s.test3_1();
        s.test4();
    }
}

```



