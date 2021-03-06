---
layout: post
title: Django Signals Comefrom
---

Aren't django signals a littel like comefrom?
-----------------------------------------------

If you do not know what a comefrom is, [wikipedia to the rescue](http://en.wikipedia.org/wiki/COMEFROM)

    In computer programming, COMEFROM (or COME FROM) is an obscure control flow
    structure used in some programming languages, primarily as a joke.
    
Some hypothetical code using comefrom,

    from goto import comefrom, label
    comefrom .repeat
    name = raw_input('what is your name? ')
    if name:
        print "Hello",name
        label .repeat
    print "Goodbye!"
    
    
And Some actual django code using signals

    class Post(models.Model):
        name = models.CharField(...)
        ...
        num_comments = models.PositiveIntegerField(default = 0)
        
    class Comment(models.Model):
        ...
        post = models.ForeignKey(Post)
        
    def handle_num_comments(sender, **kwargs):
        instance = kwargs['instance']
        instance.post.num_comments+=1
        instance.post.save()
        
    from django.db.signals import post_save
    
    post_save.connect(handle_num_comments, sender=Comment)
    
And the same code using COMEFROM

    class Post(models.Model):
        name = models.CharField(...)
        ...
        num_comments = models.PositiveIntegerField(default = 0)
        
    class Comment(models.Model):
        ...
        post = models.ForeignKey(Post)
        
        def save(self, *args, **kwargs):
            super(Comment, self).save(*args, **kwargs)
            instance = self
            LABEL .post_save
        
    def handle_num_comments(sender, **kwargs):
        instance = kwargs['instance']
        COMEFROM .post_save
        instance.post.num_comments+=1
        instance.post.save()
        
So isn't the signals code a little like COMEFROM, and why is it superior to comefrom?


    

