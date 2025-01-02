---
layout: post
section-type: post
has-comments: true
title: Hiểu đơn giản về OOP
category: tech
tags: ["tutorial", "programing"]
---

Với những ai bắt đầu học lập trình, (hay thậm chí là lập trình lâu năm) mỗi khi được hỏi về OOP có lẽ đều có chút bối rối nhất định.

OOP là một khái niệm nền tảng trong lập trình hiện đại. Nhưng tại sao nó lại quan trọng đến vậy? Và làm thế nào để chúng ta có thể tiếp cận OOP một cách dễ hiểu hơn?

Cùng khám phá thông qua các ví dụ đơn giản sau nhé.

#### Class & Objects - Lớp & Đối tượng
Khởi tạo bản sao ảo (Instance) của Đối tượng (Object) được xây dựng trên bản thiết kế (Class)
```java
class Animal {
    String title;
    
    void sound() {
        print("haha");
    }
}

Book animal = new Animal();
```

<br/>

#### Encapsulation - Đóng gói
Chúng ta chỉ thấy được những gì người khác muốn cho chúng ta thấy
```java
class Animal {
    private String title;
    private String sound;

    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
}
```
Chỉ có 2 method getTitle() và setTitle() là có thể thấy được từ bên ngoài.

<br/>

#### Inheritance - Kế thừa
Một đứa con thừa hưởng những đặc điểm từ bố mẹ
```java
class Cat extends Animal {}
```
<br/>

#### Polymorphism - Đa hình 
Override (Runtime polymophism) - Cùng là tiếng kêu của động vật nhưng tiếng con chó sẽ khác tiếng con mèo chứ nhỉ 
```java
class Cat extends Animal {
    @override
    void sound() {
        print("meow");
    }
}

class Dog extends Animal {
    @override
    void sound() {
        print("gâu gâu");
    }
}
```

Overload (complie-time polymophism) - hoặc là động vật vừa có thể kêu trong khi nhảy
```java
class Animal {
    void sound() {
        print ("haha");
    }

    void sound(String action) {
        print ("haha" + action);
    }
}
```
<br/>

#### Abstraction/Interface - Trừu tượng
Một menu các món ăn có thể được phục vụ trong nhà hàng 
```java
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    voidd sound() {
        print ("gâu gâu");
    }
}
```

Trên đây là những ví dụ và liên tưởng cực kì đơn giản về OOP, rất hi vọng phần nào giúp được các bạn trên con đường chinh phục `nghiệp code` đầy gian truân này.

