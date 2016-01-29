

# App Engine Many-to-Many Relationships

## Objectives

+ Understand what a Many-to-Many relationship symbolizes
+ Can implement such a relationship with App Engine's Datastore

## Motivation / Why Should You Care?

Often we want to represent real world concepts in code. For example we might want to store all of the tags on a tumblr photo in our database. In this case a photo can have many tags, but a tag can relate to many photo's as well. This is another very important way to represent data.

## Lesson

### Many-to-Many Models

Using our Teams model from before, let’s go over an example of a many:many relationship. A team has many fans, and a fan can support many teams. This is a many:many relationship.

We’re still are going to take advantage of the KeyProperty database type. Except this time, we'll keep track of the relationships another way. Instead of the fan belonging to the team, or the team belonging to the fan, we'll create a third model that keeps track of fans and the teams they root for. That way, if

```python
class Fan(ndb.Model):
    first_name = ndb.StringProperty()
    last_name = ndb.StringProperty()
    home_city = ndb.StringProperty()

class FanTeam(ndb.Model):
    fan = ndb.KeyProperty(Fan)
    team = ndb.KeyProperty(Team)
```

First, we need to add fans.

```python
nicki = Fan(first_name='Nicki', last_name='Anselmo', home_city='New Orleans').put()
norah = Fan(first_name='Norah', last_name='Solo', home_city='New York').put()
```

Now when we want to add a fan to a team, we create a new instance of FanTeam. We need to get our fan, get our team, and then link them.

```python
FanTeam(fan=nicki, team=da_bulls).put()
FanTeam(fan=norah, team=da_bulls).put()
```

To get all the fans of a team, we build a query on our FanTeam class:

```python
bulls_fans = Fanteam.query(team=da_bulls).fetch()
```

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/cssi-9.4-appengine-datastore-many-to-many' title='App Engine Many-to-Many Relationships'>App Engine Many-to-Many Relationships</a> on Learn.co and start learning to code for free.</p>
