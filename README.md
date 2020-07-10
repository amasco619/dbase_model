from django.db import models
from datetime import datetime

# Create your models here.
class Category(models.Model):
	text = models.CharField(max_length=50)
	details = models.TextField()
	date_added = models.DateTimeField(default=datetime.now, blank=True)
	
	class Meta:
		verbose_name_plural = 'categories'
	def __str__(self):
		return self.text
		
class Location(models.Model):
	name = models.CharField(max_length=20)
	slug = models.SlugField(unique=True)
	date_added = models.DateTimeField(default=datetime.now, blank=True)
	def __str__(self):
		return self.name
	
class JobListing(models.Model):
	category = models.ForeignKey(Category, on_delete=models.DO_NOTHING)
	location = models.ForeignKey(Location, on_delete=models.DO_NOTHING)
	company = models.CharField(max_length=50)
	title = models.CharField(max_length=100)
	description = models.TextField()
	date_added = models.DateTimeField(default=datetime.now, blank=True)
