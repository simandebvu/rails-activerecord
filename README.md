# Building with active record ROR

###### tags: `Odin Project` `Ruby on Rails` `Microverse`

> List of records with possible models, columns, validations and associations you might use to implement it. 

## :memo: Scenarios

### :rocket: Scenario 1: Online learning platform
You’ve got many different courses, each with a title and description, and each course has multiple lessons. Lesson content consists of a title and body text.

**Course**

```ruby=2.6.6
id:integer
title:string [unique, 4-20 chars, present]
description:text [present]
created_at:datetime
updated_at:datetime


has_many :lessons
```


**Lesson**

```ruby=2.6.6
id:integer
title:string [unique, 4-20 chars, present]
body:text [present]
created_at:datetime
updated_at:datetime


belongs_to :course
```


### :rocket: Scenario 2: Profile Tab
You are building the profile tab for a new user on your site. You are already storing your user’s username and email, but now you want to collect demographic information like city, state, country, age and gender. 

**Profile**

```ruby=2.6.6
id:integer
gender:text [limit 1, validates :gender,inclusion: { :in => %w( m f M F)}]  
city:string [unique, 4-20 chars, present]
state:string [unique, 4-20 chars, present]
country:string [unique, 4-20 chars, present]  
created_at:datetime
updated_at:datetime


belongs_to :user
```

### :rocket: Scenario 3: Virtual Pinboard
You want to build a virtual pinboard, so you’ll have users on your platform who can create “pins”. Each pin will contain the URL to an image on the web. Users can comment on pins (but can’t comment on comments).

**User**

```ruby=2.6.6
id:integer
username:string [unique, 4-12 chars, present]
email:string [unique, present]
password:string [6-16 chars, present]
created_at:datetime
updated_at:datetime


has_many :pins
```

**Pin**

```ruby=2.6.6
id:integer
url:string [unique, 4-20 chars, present]
created_at:datetime
updated_at:datetime


has_many :comments, through :users
```


**Comment**

```ruby=2.6.6
id:integer
title:string [unique, 4-20 chars, present]
description:text [present]
created_at:datetime
updated_at:datetime


belongs_to :user
```


### :rocket: Scenario 4: Hacker News
You want to build a message board like Hacker News. Users can post links. Other users can comment on these submissions or comment on the comments. How would you make sure a comment knows where in the hierarchy it lives?

**User**

```ruby=2.6.6
id:integer
username:string [unique, 4-12 chars, present]
email:string [unique, present]
password:string [6-16 chars, present]
created_at:datetime
updated_at:datetime


has_many :links
```

**Link**

```ruby=2.6.6
id:integer
url:string [unique, 4-20 chars, present]
created_at:datetime
updated_at:datetime

belongs_to :user
has_many :comments, through :user
```


**Comment**

```ruby=2.6.6
id:integer
title:string [unique, 4-20 chars, present]
description:text [present]
created_at:datetime
updated_at:datetime


belongs_to :user
```