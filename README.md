from django.db import models
from django.core.validators import RegexValidator, URLValidator
from django.utils import timezone


# Task 1
class Event(models.Model):
    title = models.CharField(max_length=255, verbose_name="Event Title")
    description = models.TextField(verbose_name="Event Description")
    date = models.DateTimeField(verbose_name="Event Date and Time")
    location = models.CharField(max_length=255, verbose_name="Event Location")
    image = models.ImageField(upload_to='events/', verbose_name="Event Image", blank=True, null=True)

    class Meta:
        verbose_name = "Event"
        verbose_name_plural = "Events"
        ordering = ['-date']  # Events ordered by date, newest first

    def __str__(self):
        return f"{self.title} - {self.date.strftime('%Y-%m-%d')}"

    def is_upcoming(self):
        return self.date >= timezone.now()


# Task 2
class Staff(models.Model):
    name = models.CharField(max_length=255, verbose_name="Name")
    position = models.CharField(max_length=255, verbose_name="Position")
    bio = models.TextField(verbose_name="Biography", blank=True)
    photo = models.ImageField(upload_to='staff/', verbose_name="Photo", blank=True, null=True)

    class Meta:
        verbose_name = "Staff"
        verbose_name_plural = "Staff"
        ordering = ['name']  # Staff members ordered alphabetically by name

    def __str__(self):
        return f"{self.name} - {self.position}"


# Task 3
class Gallery(models.Model):
    title = models.CharField(max_length=255, verbose_name="Title")
    description = models.TextField(verbose_name="Description", blank=True, null=True)
    image = models.ImageField(upload_to='gallery/', verbose_name="Image")

    class Meta:
        verbose_name = "Gallery"
        verbose_name_plural = "Galleries"
        ordering = ['title']  # Galleries ordered by title

    def __str__(self):
        return self.title


# Task 4
class Contact(models.Model):
    phone_regex = RegexValidator(regex=r'^\+?1?\d{9,15}$', message="Phone number must be entered in the format: '+999999999'. Up to 15 digits allowed.")
    
    name = models.CharField(max_length=255, verbose_name="Name")
    address = models.CharField(max_length=255, verbose_name="Address", blank=True, null=True)
    phone = models.CharField(validators=[phone_regex], max_length=15, verbose_name="Phone", blank=True, null=True)
    email = models.EmailField(verbose_name="Email", blank=True, null=True)
    website = models.URLField(validators=[URLValidator], verbose_name="Website", blank=True, null=True)

    class Meta:
        verbose_name = "Contact"
        verbose_name_plural = "Contacts"
        ordering = ['name']  # Contacts ordered by name

    def __str__(self):
        return self.name
