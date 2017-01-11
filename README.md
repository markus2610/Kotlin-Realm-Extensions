# Kotlin-Realm-Extensions

Kotlin extensions for simplifying Realm API.

## Features

Store, Query and Delete operations in Realm requires a bit of bolilerplate. With Kotlin Realm Extensions, you can simplify your code to its minimum expression.

## Download

Grab via Gradle:
```groovy
repositories {
    mavenCentral()
}

compile 'com.github.vicpinm:krealmextensions:1.0.0'
```

## Usage
### Store entities

All your entities should extend RealmObject.

#### Before (java)
````
User user = new User("John");

Realm realm = Realm.getDefaultInstance();
realm.beginTransaction();
realm.copyToRealmOrUpdate(user);  
realm.commitTransaction();
realm.close();
````
#### After (Kotlin + extensions)

````
User("John").save()
````

#### Save list: Before (java)
````
List<User> users = new ArrayList<User>(...);

Realm realm = Realm.getDefaultInstance();
realm.beginTransaction();
realm.copyToRealmOrUpdate(users);  
realm.commitTransaction();
realm.close();
````
#### Save list: After (Kotlin + extensions)

````
listOf<User>(...).saveAll()
````

Save method creates or updates your entity into database. You can also use create() method, which only create a new entity into database. If a previous one exists with the same primary key, it will throw a exception.

### Query entities

All query extensions return detached realm objects, using copyFromRealm() method. 

#### Get first entity: Before (java)
````
Realm realm = Realm.getDefaultInstance();
Event firstEvent = realm.where(Event.class).findFirst();
firstEvent = realm.copyFromRealm(event);
realm.close();
````
#### Get first entity: After (Kotlin + extensions)
````
val firstEvent = Event().firstItem
````

You can use lastItem extension too.

#### Get all entities: Before (java)
````
Realm realm = Realm.getDefaultInstance();
List<Event> events = realm.where(Event.class).findAll();
events = realm.copyFromRealm(event);
realm.close();
````
#### Get  all entities: After (Kotlin + extensions)
````
val events = Event().allItems
````

#### Get entities with conditions: Before (java)
````
Realm realm = Realm.getDefaultInstance();
List<Event> events = realm.where(Event.class).equalTo("id",1).findAll();
events = realm.copyFromRealm(event);
realm.close();
````

#### Get entities with conditions: After (Kotlin + extensions)
````
val events = Event().where { query -> query.equalTo("id",1) }
````

### Delete entities
