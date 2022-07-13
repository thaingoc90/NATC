Setup ATC 
1. Install python pip (require version python2.7): sudo apt install python-pip
2. Install django 1.10 : pip install django==1.10
3. Install project: sudo make install
4. Create project atcui (if not existed): django-admin startproject atcui
5. Change setting atcui base on file Setup.md or README.md
	+ Follow setup from Setup.md or README.md
	+ Should update ALLOWED_HOSTS if use hotspot
		ALLOWED_HOSTS = [
		  'localhost',
		  '127.0.0.1',
		  '<hotspot ip>']
6. Run atcd & server atcui
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