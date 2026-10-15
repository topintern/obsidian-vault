---
kind: "coding-problem"
title: "Mediator (Day 9)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/Mediator.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Mediator (Day 9)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Mediator design pattern
 
This pattern defines a separate (mediator) object that encapsulates the interaction between a set of objects and the objects delegate their interaction to a mediator object instead of interacting with each other directly.


Design participants
Mediator – defines the interface for communication between Colleague objects

ConcreteMediator – implements the Mediator interface and coordinates communication between Colleague objects. It is aware of all of the Colleagues and their purposes with regards to inter-communication.

Colleague – defines the interface for communication with other Colleagues through its Mediator

ConcreteColleague – implements the Colleague interface and communicates with other Colleagues through its 
Mediator

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Mediator.java
> ```java
> /*
>  * 
>  * 
> Mediator design pattern
>  
> This pattern defines a separate (mediator) object that encapsulates the interaction between a set of objects and the objects delegate their interaction to a mediator object instead of interacting with each other directly.
>
>
> Design participants
> Mediator – defines the interface for communication between Colleague objects
>
> ConcreteMediator – implements the Mediator interface and coordinates communication between Colleague objects. It is aware of all of the Colleagues and their purposes with regards to inter-communication.
>
> Colleague – defines the interface for communication with other Colleagues through its Mediator
>
> ConcreteColleague – implements the Colleague interface and communicates with other Colleagues through its 
> Mediator
>
>
>  */
>
> package DesignPatterns.MediatorPattern;
> import java.util.HashMap;
> import java.util.Map;
>
>
> // Mediator Interface
>  interface IChatRoom 
> {
>     public void sendMessage(String msg, String userId);
>  
>     void addUser(User user);
> }
>  
>  // Concrete Mediator
>  
>  class ChatRoom implements IChatRoom {
>  
>     private Map<String, User> usersMap = new HashMap<>();
>  
>     @Override
>     public void sendMessage(String msg, String userId) 
>     {
>         User u = usersMap.get(userId);
>         u.receive(msg);
>     }
>  
>     @Override
>     public void addUser(User user) {
>         this.usersMap.put(user.getId(), user);
>     }
> }
>
> // Colleague Class
>  
>  abstract class User
> {
>     private IChatRoom mediator;
>      
>     private String id;
>     private String name;
>      
>     public User(IChatRoom room, String id, String name){
>         this.mediator = room;
>         this.name = name;
>         this.id = id;
>     }
>      
>     public abstract void send(String msg, String userId);
>     public abstract void receive(String msg);
>  
>     public IChatRoom getMediator() {
>         return mediator;
>     }
>  
>     public String getId() {
>         return id;
>     }
>  
>     public String getName() {
>         return name;
>     }
> }
>
> // Concrete Colleagues
>
>  class ChatUser extends User {
>      
>     public ChatUser(IChatRoom room, String id, String name) {
>         super(room, id, name);
>     }
>  
>     @Override
>     public void send(String msg, String userId) {
>         System.out.println(this.getName() + " :: Sending Message : " + msg);
>         getMediator().sendMessage(msg, userId);
>     }
>  
>     @Override
>     public void receive(String msg) {
>         System.out.println(this.getName() + " :: Received Message : " + msg);
>     }
>  
> }
>
>
> // Test the mediator pattern.
>
>  class Mediator {
> 	
> 	 public static void main(String[] args) 
> 	    {
> 	        IChatRoom chatroom = new ChatRoom();
> 	         
> 	        User user1 = new ChatUser(chatroom,"1", "Alex");
> 	        User user2 = new ChatUser(chatroom,"2", "Brian");
> 	        User user3 = new ChatUser(chatroom,"3", "Charles");
> 	        User user4 = new ChatUser(chatroom,"4", "David");
> 	         
> 	        chatroom.addUser(user1);
> 	        chatroom.addUser(user2);
> 	        chatroom.addUser(user3);
> 	        chatroom.addUser(user4);
> 	 
> 	        user1.send("Hello brian", "2");
> 	        user2.send("Hey buddy", "1");
> 	    }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%209%20Solutions/Mediator.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/Mediator.java
