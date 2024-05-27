Setup ATC 
1. Install python pip (require version python2.7): sudo apt install python-pip
2. Install django 1.10 : pip install django==1.10
3. Install project: sudo make install
4. Create project atcui (if not existed): django-admin startproject atcui
5. Change setting atcui base on file Setup.md or README.md
	+ open atcui/settings.py and enable the ATC apps by adding to INSTALLED_APPS:

       INSTALLED_APPS = (
		    ...
		    # Django ATC API
		    'rest_framework',
		    'atc_api',
		    # Django ATC Demo UI
		    'bootstrap_themes',
		    'django_static_jquery',
		    'atc_demo_ui',
		    # Django ATC Profile Storage
		    'atc_profile_storage',
		) 
	+ open atcui/urls.py and enable routing to the ATC apps by adding the routes to urlpatterns:

		from django.views.generic.base import RedirectView

		from django.conf.urls import include
		
		urlpatterns = [
		    ...
		    # Django ATC API
		    url(r'^api/v1/', include('atc_api.urls')),
		    # Django ATC Demo UI
		    url(r'^atc_demo_ui/', include('atc_demo_ui.urls')),
		    # Django ATC profile storage
		    url(r'^api/v1/profiles/', include('atc_profile_storage.urls')),
		    url(r'^$', RedirectView.as_view(url='/atc_demo_ui/', permanent=False)),
		]
	+ Should update ALLOWED_HOSTS if use hotspot
		ALLOWED_HOSTS = [
		  'localhost',
		  '127.0.0.1',
		  '<hotspot ip>']
	+ update the Django DB:
		python manage.py migrate
6. Run atcd & server atcui:
	
 	sudo atcd --atcd-wan <wan-profile-name> --atcd-lan <lan-profile-name> --atcd-mode unsecure
	
 	./atc/atcui/manage.py runserver 0.0.0.0:8080
7. Example Profile
{
  "down": {
        "rate": null,
        "loss": {
            "percentage": 0.0,
            "correlation": 0.0
        },
        "delay": {
            "delay": 0,
            "jitter": 0,
            "correlation": 0.0
        },
        "corruption": {
            "percentage": 0.0,
            "correlation": 0.0
        },
        "reorder": {
            "percentage": 0.0,
            "correlation": 0.0,
            "gap": 0
        },
        "iptables_options": ["-s 120.138.69.180 -p udp --sport 4135"]
    },
    "up": {
        "rate": null,
        "loss": {
            "percentage": 0.0,
            "correlation": 0.0
        },
        "delay": {
            "delay": 0,
            "jitter": 0,
            "correlation": 0.0
        },
        "corruption": {
            "percentage": 0.0,
            "correlation": 0.0
        },
        "reorder": {
            "percentage": 0.0,
            "correlation": 0.0,
            "gap": 0
        },
        "iptables_options": ["-d 120.138.74.196 -p udp --dport 4135"]
    }
}
