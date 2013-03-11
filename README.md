mirocommunity_appsembler
========================

This is a Mirocommunity project template that can be deployed to Appsembler. See http://mirocommunity.org for an example of a Mirocommunity site and the original code is available at https://github.com/pculture/mirocommunity/.

API keys
--------

Need to set the following as environment variables that are loaded in settings.py::

# Vimeo
VIMEO_API_KEY
VIMEO_API_SECRET 

# UStream key
USTREAM_API_KEY

# recaptcha keys
RECAPTCHA_PUBLIC_KEY
RECAPTCHA_PRIVATE_KEY

# Facebook options
FACEBOOK_APP_ID
FACEBOOK_API_SECRET

# Twitter options
TWITTER_CONSUMER_KEY
TWITTER_CONSUMER_SECRET

Celery
------

Need to set up Celery in order to do the video harvesting. In settings.py::

	import djcelery
	djcelery.setup_loader()
	CELERY_TASK_SERIALIZER = 'json'
	# Comment these lines out to use a celery server.
	CELERY_ALWAYS_EAGER = True
	CELERY_EAGER_PROPAGATES_EXCEPTIONS = True

ElasticSearch
-------------

For Haystack, need to set up ElasticSearch (or Whoosh) to provide search capabilities. In settings.py::

	SEARCH = os.environ.get('SEARCH')
	if SEARCH == 'elasticsearch':
	    HAYSTACK_CONNECTIONS = {
	        'default': {
	            'ENGINE': 'haystack.backends.elasticsearch_backend.ElasticsearchSearchEngine',
	            'URL': 'http://localhost:9200/',
	            'INDEX_NAME': 'mirocommunity'
	        }
	    }
